# 3. La biblioteca de soporte de Android

## Contenido:
  * [Acerca de la biblioteca de soporte de Android](#acerca)
  * [Librerías de apoyo y características](#librerias)
  * [Configuración y uso de la librería de soporte de Android](#configuracion)
  * [Comprobando las versiones del sistema.](#versiones)
  * [Prácticas relacionadas](#practicas)
  * [Aprende más](#aprende)

En este capítulo, se explora la biblioteca de soporte de Android, que forma parte de las herramientas del SDK de Android. Sep uede usar la biblioteca de soporte de Android para obtener versiones compatibles con versiones anteriores de las nuevas funciones de Android ó más elementos de la interfaz de usuario (IU) no incluidos en el framework estándar de Android.

### <a id="acerca"></a>Acerca de la biblioteca de soporte de Android

Las herramientas del SDK de Android incluyen una serie de librerías llamadas colectivamente la **Librería de soporte de Android**. Este paquete de librerías proporcionan varias características que no están integradas en el framework estándar de Android y proporciona compatibilidad con versiones anteriores para dispositivos más antiguos. Se debe incluir cualquiera de estas librerías en una aplicación para incorporar su funcionalidad.
*Nota*: la librería de soporte de Android es un paquete diferente de la librería de soporte de testeo de Android. La librería de soporte de pruebas proporciona herramientas y API solo para los testeos, mientras que la librería de soporte más general proporciona características de todo tipo (pero no de prueba).

#### Caracteristicas

Las características de la biblioteca de soporte de Android incluyen:
  * Versiones de componentes de framework compatibles con versiones anteriores. Estas bibliotecas de compatibilidad le permiten usar características y componentes disponibles en las versiones más recientes de la plataforma Android, incluso cuando su aplicación se ejecuta en una versión anterior de la plataforma. Por ejemplo, los dispositivos más antiguos pueden no tener acceso a características más nuevas, como fragments, barras de aplicaciones (también conocidas como *action bars*) o elementos de diseño de materiales. La biblioteca de soporte proporciona acceso a esas funciones en dispositivos más antiguos.
  * Layouts adicionales y elementos de la interfaz de usuario. La biblioteca de soporte incluye vistas y layouts que pueden ser útiles para una aplicación, pero no están incluidos en el framework estándar de Android. Por ejemplo, la vista **RecyclerView** es parte de la biblioteca de soporte.
  * Soporte para diferentes factores de forma de dispositivos, como TV o wearables: por ejemplo, la librería **Leanback** incluye componentes específicos para el desarrollo de aplicaciones en dispositivos de TV.
  * Soporte de diseño: la biblioteca de soporte de diseño incluye componentes para admitir elementos de Material Design en una aplicación, incluidos los **botones flotantes (FAB)**. 
  * Otras características, como soporte de paleta, anotaciones, dimensiones de diseño basadas en porcentajes y preferencias.

#### Compatibilidad con versiones anteriores

Las bibliotecas de soporte permiten que las aplicaciones que se ejecutan en versiones anteriores de la plataforma Android admitan las funciones disponibles en las versiones más recientes de la plataforma. Por ejemplo, una aplicación que se ejecuta en una versión de Android inferior a 5.0 (nivel de API 21) que se basa en clases de framework no puede mostrar elementos de Material Design, ya que esa versión del framework de Android no es compatible con Material Design. Sin embargo, si la aplicación incorpora la biblioteca *v7 appcompat*, la aplicación tiene acceso a muchas de las funciones disponibles en el nivel 21 de la API, incluida la compatibilidad con Material Design. Como resultado, su aplicación puede ofrecer una experiencia más consistente en una amplia gama de versiones de plataforma.

Las API de la biblioteca de soporte también proporcionan una capa de compatibilidad entre diferentes versiones de las API del framework. Esta capa de compatibilidad intercepta de forma transparente las llamadas a la API y cambia los argumentos que se pasan, maneja la operación en sí misma o redirige la operación. En el caso de las bibliotecas de soporte, al utilizar los métodos de la capa de compatibilidad, puede garantizar la interoperabilidad entre las versiones de Android más antiguas y más nuevas. Cada nueva versión de Android agrega nuevas clases y métodos, y posiblemente deja de usar algunas clases y métodos más antiguos. Las bibliotecas de soporte incluyen clases de compatibilidad que pueden usarse para la compatibilidad con versiones anteriores. Puede identificar estas clases por sus nombres, que incluyen "Compat" (como *ActivityCompat*).

Cuando una aplicación llama a uno de los métodos de la clase de soporte, el comportamiento de ese método depende de la versión de Android que corre por debajo. Si el dispositivo incluye la funcionalidad de f amework necesaria, la librería de soporte usa el framework. Por el contrario, si el dispositivo está ejecutando una versión anterior de Android, la librería de soporte intenta implementar un comportamiento compatible similar con las API que tiene disponibles.

Para la mayoría de los casos, no necesita escribir código complejo que verifique la versión de Android y realice diferentes operaciones basadas en esa versión. Puede confiar en la librería de soporte para realizar esas comprobaciones y elegir el comportamiento adecuado.

En caso de duda, se debe elegir una clase de compatibilidad de la librería de soporte sobre la versión de Android disponible.

#### Versiones

Cada paquete en la librería de soporte tiene un número de versión en tres partes (x.y.z) que corresponde a un nivel de API de Android y a una revisión particular de esa librería. Por ejemplo, un número de versión de la librería de soporte de 22.3.4 es la versión 3.4 de la biblioteca de soporte para API 22.

Como regla general, se debe usar la versión más reciente de la librería de soporte para la API que compila la aplicación. Por ejemplo, si su aplicación apunta a la API 26, use la versión 26.x.x de la librería de soporte.

Siempre puede usar una librería de soporte más nueva que la de su API objetivo. Por ejemplo, si su aplicación apunta a la API 22, puede usar la versión 25 o superior de la biblioteca de soporte. Por el contrario no se puede usar una librería de soporte anterior con una API más nueva. Como regla general, debe tratar de usar la API más actualizada y las librerías de soporte en cualquier aplicación.

#### Niveles API

Además del número de versión real, el nombre de la propia librería de soporte indica el nivel de API con el que la librería es compatible con versiones anteriores. No puede usar una librería de soporte en una aplicación para una API más alta que la API mínima que admite su aplicación. Por ejemplo, si la API mínima que admite su aplicación es 10, no puede usar la librería de soporte v13 o la librería de soporte de preferencias v14 en su aplicación. Si su aplicación utiliza varias librerías de soporte, su API mínima debe ser mayor que la cantidad más grande, es decir, si incluye bibliotecas de soporte para v7, v13 y v14, su API mínima debe ser de al menos 14.

Todas las bibliotecas de soporte, incluidas las bibliotecas v4 y v7, requieren un SDK mínimo de API 9.

### <a id="librerias"></a> Librerías de soporte y características

Esta sección describe las características importantes proporcionadas por las bibliotecas en la biblioteca de soporte de Android. Aprenderá sobre muchas de las funciones descritas en esta sección en otros capítulos.

#### librería de soporte v4

Las librerías de soporte v4 incluyen el conjunto más grande de API en comparación con las otras librerías, incluido el soporte para componentes de aplicaciones, funciones de interfaz de usuario, accesibilidad, manejo de datos, conectividad de red y utilidades de programación.

Las librerías de soporte de v4 incluyen estos componentes específicos:

  * **v4 compat library**: wrappers de compatibilidad (clases que incluyen la palabra "Compat") para una serie de APIs de infraestructura básica.
  * **Librería v4 core-utils**: proporciona varias clases de utilidades
  * **Librería v4 core-ui**: implementa una variedad de componentes relacionados con la interfaz de usuario.
  * **Librería v4 media-compat**: Partes de **backport** para la infraestructura de medios desde la API 21.
  * **Librería de fragments v4**: agrega soporte para fragments de Android.

#### librería de soporte v7

La librería de soporte de v7 incluye tanto librerías de compatibilidad como características adicionales.

La librería de soporte de v7 incluye todas las bibliotecas de soporte de v4, por lo que no tiene que agregarlas por separado. Se incluye una dependencia de la librería de soporte de v7 por defecto en cada nuevo proyecto de Android Studio, y las nuevas actividades en un proyecto se extienden desde **AppCompatActivity**.

Las bibliotecas de soporte de v7 incluyen estos componentes específicos:

   * **Librería v7 appcompat**: agrega soporte para el patrón de diseño de la interfaz de usuario de la barra de aplicaciones y soporte para implementaciones de Material Design UI.
   * **Librería v7 cardview**: proporciona la clase **CardView**, una vista que permite mostrar información dentro de tarjetas.
   * **Librería v7 gridlayout**: incluye la clase **GridLayout**, que le permite organizar los elementos de la interfaz de usuario utilizando una cuadrícula de celdas rectangulares
   * **Librería v7 mediarouter**: proporciona **MediaRouter** y clases de medios relacionados que admiten Google Cast.
   * **Librería v7 palette**: implementa la clase **Palette**, que le permite extraer colores prominentes de una imagen.
   * **Librería v7 recyclerview**: proporciona la clase **RecyclerView**, una vista para mostrar de manera eficiente grandes conjuntos de datos al proporcionar una ventana limitada de elementos de datos.
   * **Librería de preferencias v7**: proporciona API para admitir objetos de **preferencias** en la configuración de la aplicación.

#### Otras bibliotecas

  * **Librería de renderización de v8**: agrega compatibilidad con **RenderScript**, un framework para ejecutar tareas intensivas en computación con un alto rendimiento.
  * **Librería de soporte v13**: proporciona soporte para usar un fragment con la clase **FragmentCompat** y clases de soporte de fragments adicionales.
  * **Librería de soporte de preferencias v14 y librería de soporte de preferencias v17 para TV**: proporciona API para agregar soporte para interfaces de preferencias en dispositivos móviles y TV.
  * **Librería leanback v17**: proporciona API para admitir la creación de Interfaces de Usuario en dispositivos de TV.
  * **Librería de soporte de anotaciones**: contiene API para admitir la adición de metadatos de anotación a sus aplicaciones.
  * **Librería de soporte de diseño**: agrega soporte para varios componentes y patrones de Material Design, como Navigation Drawers, botones flotantes (FAB), snack bars y pestañas.
  * **Librería de soporte de pestañas personalizadas**: agrega soporte para agregar y administrar pestañas personalizadas en las aplicaciones.
  * **Librería de soporte de porcentaje**: le permite agregar y administrar dimensiones basadas en porcentajes en su aplicación.
  * **Librería de soporte de recomendaciones de aplicaciones para TV**: proporciona API para agregar recomendaciones de contenido en su aplicación que se ejecuta en dispositivos de TV.

### <a id="configuracion"></a>Configuración y uso de la biblioteca de soporte de Android

El paquete de la librería de soporte de Android es parte del SDK de Android y está disponible para descargarlo en el administrador del SDK de Android. Para configurar un proyecto para usar cualquiera de las librerías de soporte, siga estos pasos:

  1. Descargue la librería de soporte con el administrador de SDK de Android o verifique que las librerías de soporte ya estén disponibles.
  2. Encuentre la declaración de dependencia de la librería para la biblioteca de soporte en la que está interesado.
  3. Agregue esa declaración de dependencia a la sección de dependencias de su archivo build.gradle (Module:app).

#### Descarga la biblioteca de soporte

En Android Studio, utilizará el repositorio de soporte de Android (el repositorio en el administrador de SDK para todas las librerías de soporte), para obtener acceso a la biblioteca desde su proyecto.

Es posible que ya tenga las librerías de soporte de Android descargadas e instaladas con Android Studio. Para verificar que tiene las librerías de soporte disponibles, siga estos pasos:

  1. En Android Studio, seleccione **Tools>Android>SDK Manager** o haga clic en el ícono del icono Administrador de SDK.![Android SDK Manager](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/3-3-c-the-android-support-library/ic_sdk_mgr.png)

     Haga clic en la pestaña Herramientas del SDK y expanda Soporte Repositorio, como se muestra en la figura a continuación.
