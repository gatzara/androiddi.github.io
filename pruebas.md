# Probando la aplicación
## Contenido:
    Acerca de las pruebas
    Configuración de pruebas
    Creación y ejecución de pruebas unitarias.
    Práctica relacionada
    Aprende más

En este capítulo, se obtiene una descripción general de las pruebas de Android y se aprenden a crear y ejecutar pruebas de unidades locales en Android Studio con JUnit.

Acerca de las pruebas

A parte de tener que comprobar cómo una aplicación se compila y se ejecuta y se ve como se visualiza en diferentes dispositivos, se debe asegurar también  que la aplicación se comporte de la manera que se espera en cada situación, especialmente a medida que su aplicación crece y cambia. Incluso si intenta probar una aplicación manualmente cada vez que realiza un cambio, ello conlleva una perspectiva tediosa en el mejor de los casos, en el peor se puede perder algo o no anticipar lo que los usuarios finales podrían hacer con su aplicación para hacer que falle.

Escribir y ejecutar pruebas es una parte crítica del proceso de desarrollo de software. El desarrollo dirigido por pruebas (TDD) es una filosofía popular de desarrollo de software que coloca las pruebas en el núcleo de todo el desarrollo de software para una aplicación o servicio. Esto no niega la necesidad de realizar más pruebas, simplemente le brinda una base de referencia sólida con la que trabajar.

Probar el código puede ayudar a detectar problemas al inicio del desarrollo, cuando son los menos costosos de abordar, y mejorar la solidez de su código a medida que la aplicación se hace más grande y más compleja. Con las pruebas en su código, puede ejercitar pequeñas porciones de su aplicación de forma aislada y de manera automatizable y repetible para realizar pruebas más eficientes.

El código que se escribe para probar una aplicación no termina en la versión de producción de la aplicación; sino que va ligado  junto con el código de su aplicación en Android Studio.

Tipos de pruebas

Android es compatible con varios tipos diferentes de pruebas y marcos de prueba. Dos formas básicas de pruebas que soporta Android Studio son las pruebas unitarias y las pruebas instrumentales.

Las pruebas unitarias son pruebas que se compilan y ejecutan completamente en una máquina local con la Máquina Virtual de Java (JVM). Use las pruebas unitarias para probar las partes de su aplicación (como la lógica interna) que no necesitan acceso al marco de Android o un dispositivo o emulador con Android, o aquellas para las que puede crear falsos objectos ("mockups" o "stub") que pretenden comportarse como los equivalentes del entorno.

Las pruebas instrumentales son pruebas que se ejecutan en un dispositivo o emulador con Android. Estas pruebas tienen acceso al marco de Android y a la información de **instrumentación**, como el **contexto** de la aplicación. Puede usar pruebas instrumentadas para pruebas unitarias, pruebas de interfaz de usuario (UI) o pruebas de integración, asegurándose de que los componentes de su aplicación interactúen correctamente con otras aplicaciones. Más comúnmente, se usaa pruebas instrumentales para las pruebas de interfaz de usuario, lo que le permite probar que su aplicación se comporta correctamente cuando un usuario interactúa con su aplicación o ingresa una entrada específica.

Para la mayoría de las formas de prueba de interfaz de usuario, se utiliza el framework *Espresso*, que le permite escribir pruebas de interfaz de usuario automatizadas. 

Examen de la unidad

Las pruebas unitarias deben ser las pruebas fundamentales en su estrategia de prueba de aplicaciones. Al crear y ejecutar pruebas unitarias con su código, puede verificar que la lógica de las áreas o unidades de códigos funcionales individuales es correcta. La ejecución de pruebas unitarias después de cada compilación le ayuda a detectar y solucionar problemas introducidos por cambios de código en su aplicación.

Una prueba de unidad generalmente ejerce la funcionalidad de la unidad de código más pequeña posible (que podría ser un método, clase o componente) de manera repetible. Cree pruebas unitarias cuando necesite verificar la lógica de un código específico en su aplicación. Por ejemplo, si prueba una clase por unidad, su prueba podría verificar que la clase se encuentra en el estado correcto. Para un método, puede probar su comportamiento para diferentes valores de sus parámetros, especialmente focalizando la gestión de valores nulos.

Por lo general, el test unitario se prueba de forma aislada y su prueba monitorea los cambios solo en esa unidad. Puede usar un marco de simulacro como **Mockito** para aislar su unidad de sus dependencias. También puede escribir sus pruebas de unidad para Android en **JUnit4**, un marco de prueba de unidad común para código Java.

La biblioteca de soporte de pruebas de Android

La biblioteca de compatibilidad de pruebas de Android proporciona la infraestructura y las API para probar aplicaciones de Android, incluida la compatibilidad con JUnit4. Con la biblioteca de compatibilidad de pruebas, puede crear y ejecutar código de prueba para sus aplicaciones.

Es posible que ya tenga instalada la biblioteca de compatibilidad de pruebas de Android con Android Studio. Para verificar el repositorio de soporte de Android, sigue estos pasos:

  1. En Android Studio, seleccione **Tools>Android>SDK Manager**
  2. Haga clic en la pestaña **SDK Tools** y busque el *Support Repository*.
  3. Si es necesario, actualice o instale la libreria.

Las clases de la Biblioteca de compatibilidad de pruebas de Android se encuentran en el paquete *android.support.test*. También hay una API de prueba más antigua en *android.test*. Debe usar las bibliotecas de soporte primero, cuando se le ofrezca una opción entre las bibliotecas de soporte y las API más antiguas, ya que las bibliotecas de soporte ayudan a crear y distribuir pruebas de una manera más limpia y confiable que la codificación directa contra la API en sí.

Ajuste
