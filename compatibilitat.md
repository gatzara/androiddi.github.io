# La biblioteca de soporte de Android

## Contenido:
  * Acerca de la biblioteca de soporte de Android
  * Bibliotecas de apoyo y características
  * Configuración y uso de la biblioteca de soporte de Android
  * Comprobando las versiones del sistema.
  * Práctica relacionada
  * Aprende más

En este capítulo, se explora la biblioteca de soporte de Android, que forma parte de las herramientas del SDK de Android. Puede usar la biblioteca de soporte de Android para obtener versiones compatibles con versiones anteriores de las nuevas funciones de Android, más elementos de la interfaz de usuario (IU) no incluidos en el marco estándar de Android.

Acerca de la biblioteca de soporte de Android

Las herramientas del SDK de Android incluyen una serie de bibliotecas llamadas colectivamente la Biblioteca de soporte de Android. Este paquete de bibliotecas proporciona varias características que no están integradas en el marco estándar de Android y proporciona compatibilidad con versiones anteriores para dispositivos más antiguos. Incluya cualquiera de estas bibliotecas en su aplicación para incorporar la funcionalidad de esa biblioteca.
Nota: la biblioteca de soporte de Android es un paquete diferente de la biblioteca de soporte de pruebas de Android que conoció en otro capítulo. La biblioteca de soporte de pruebas proporciona herramientas y API solo para las pruebas, mientras que la biblioteca de soporte más general proporciona características de todo tipo (pero no de prueba).

Caracteristicas

Las características de la biblioteca de soporte de Android incluyen:

    Versiones de componentes de framework compatibles con versiones anteriores. Estas bibliotecas de compatibilidad le permiten usar características y componentes disponibles en las versiones más recientes de la plataforma Android, incluso cuando su aplicación se ejecuta en una versión anterior de la plataforma. Por ejemplo, los dispositivos más antiguos pueden no tener acceso a características más nuevas, como fragmentos, barras de aplicaciones (también conocidas como barras de acción) o elementos de diseño de materiales. La biblioteca de soporte proporciona acceso a esas funciones en dispositivos más antiguos.
    Diseño adicional y elementos de la interfaz de usuario. La biblioteca de soporte incluye vistas y diseños que pueden ser útiles para su aplicación, pero no están incluidos en el marco estándar de Android. Por ejemplo, la vista RecyclerView que usará en otro capítulo es parte de la biblioteca de soporte.
    Soporte para diferentes factores de forma de dispositivos, como TV o wearables: por ejemplo, la biblioteca Leanback incluye componentes específicos para el desarrollo de aplicaciones en dispositivos de TV.
    Soporte de diseño: la biblioteca de soporte de diseño incluye componentes para admitir elementos de Diseño de materiales en su aplicación, incluidos los botones de acción flotante (FAB). Aprenderás más sobre Material Design en un capítulo posterior.
    Varias otras características, como soporte de paleta, anotaciones, dimensiones de diseño basadas en porcentajes y preferencias.

Compatibilidad con versiones anteriores

Las bibliotecas de soporte permiten que las aplicaciones que se ejecutan en versiones anteriores de la plataforma Android admitan las funciones disponibles en las versiones más recientes de la plataforma. Por ejemplo, una aplicación que se ejecuta en una versión de Android inferior a 5.0 (nivel de API 21) que se basa en clases de marco no puede mostrar elementos de Diseño de materiales, ya que esa versión del marco de Android no es compatible con Diseño de materiales. Sin embargo, si la aplicación incorpora la biblioteca v7 appcompat, esa aplicación tiene acceso a muchas de las funciones disponibles en el nivel 21 de la API, incluida la compatibilidad con Material Design. Como resultado, su aplicación puede ofrecer una experiencia más consistente en una amplia gama de versiones de plataforma.

Las API de la biblioteca de soporte también proporcionan una capa de compatibilidad entre diferentes versiones de las API del marco. Esta capa de compatibilidad intercepta de forma transparente las llamadas a la API y cambia los argumentos que se pasan, maneja la operación en sí misma o redirige la operación. En el caso de las bibliotecas de soporte, al utilizar los métodos de la capa de compatibilidad, puede garantizar la interoperabilidad entre las versiones de Android más antiguas y más nuevas. Cada nueva versión de Android agrega nuevas clases y métodos, y posiblemente deja de usar algunas clases y métodos más antiguos. Las bibliotecas de soporte incluyen clases de compatibilidad que pueden usarse para la compatibilidad con versiones anteriores. Puede identificar estas clases por sus nombres, que incluyen "Compat" (como ActivityCompat).

Cuando una aplicación llama a uno de los métodos de la clase de soporte, el comportamiento de ese método depende de la versión de Android subyacente. Si el dispositivo incluye la funcionalidad de marco necesaria, la biblioteca de soporte usa el marco. Si el dispositivo está ejecutando una versión anterior de Android, la biblioteca de soporte intenta implementar un comportamiento compatible similar con las API que tiene disponibles.

Para la mayoría de los casos, no necesita escribir código complejo que verifique la versión de Android y realice diferentes operaciones basadas en esa versión. Puede confiar en la biblioteca de asistencia para realizar esas comprobaciones y elegir el comportamiento adecuado.

En caso de duda, elija una clase de compatibilidad de biblioteca de soporte sobre la clase de marco.

Versiones

Cada paquete en la biblioteca de soporte tiene un número de versión en tres partes (x.y.z) que corresponde a un nivel de API de Android y a una revisión particular de esa biblioteca. Por ejemplo, un número de versión de la biblioteca de soporte de 22.3.4 es la versión 3.4 de la biblioteca de soporte para API 22.

Como regla general, use la versión más reciente de la biblioteca de soporte para el
