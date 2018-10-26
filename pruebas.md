# Probando la aplicación
## Contenido:
* [Acerca de las pruebas](#acerca)
* [Configuración de pruebas](#configuracion)
* [Creación y ejecución de pruebas unitarias](#creacion).
* [Prácticas relacionadas](#practicas)
* [Aprende más](#aprende)

En este capítulo, se obtiene una descripción general de las pruebas de Android y se aprenden a crear y ejecutar pruebas de unidades locales en Android Studio con JUnit.

### <a id="acerca"></a>Acerca de las pruebas

A parte de tener que comprobar cómo una aplicación se compila y se ejecuta y se ve como se visualiza en diferentes dispositivos, se debe asegurar también  que la aplicación se comporte de la manera que se espera en cada situación, especialmente a medida que su aplicación crece y cambia. Incluso si intenta probar una aplicación manualmente cada vez que realiza un cambio, ello conlleva una perspectiva tediosa en el mejor de los casos, en el peor se puede perder algo o no anticipar lo que los usuarios finales podrían hacer con su aplicación para hacer que falle.

Escribir y ejecutar pruebas es una parte crítica del proceso de desarrollo de software. El [desarrollo dirigido por pruebas (TDD)](https://en.wikipedia.org/wiki/Test-driven_development) es una filosofía popular de desarrollo de software que coloca las pruebas en el núcleo de todo el desarrollo de software para una aplicación o servicio. Esto no niega la necesidad de realizar más pruebas, simplemente le brinda una base de referencia sólida con la que trabajar.

Probar el código puede ayudar a detectar problemas al inicio del desarrollo, cuando son los menos costosos de abordar, y mejorar la solidez de su código a medida que la aplicación se hace más grande y más compleja. Con las pruebas en su código, puede ejercitar pequeñas porciones de su aplicación de forma aislada y de manera automatizable y repetible para realizar pruebas más eficientes.

El código que se escribe para probar una aplicación no termina en la versión de producción de la aplicación; sino que va ligado  junto con el código de su aplicación en Android Studio.

#### Tipos de pruebas

Android es compatible con varios tipos diferentes de pruebas y marcos de prueba. Dos formas básicas de pruebas que soporta Android Studio son las pruebas unitarias y las pruebas instrumentales.

Las pruebas unitarias son pruebas que se compilan y ejecutan completamente en una máquina local con la Máquina Virtual de Java (JVM). Use las pruebas unitarias para probar las partes de su aplicación (como la lógica interna) que no necesitan acceso al marco de Android o un dispositivo o emulador con Android, o aquellas para las que puede crear falsos objectos ("mockups" o "stub") que pretenden comportarse como los equivalentes del entorno.

Las pruebas instrumentales son pruebas que se ejecutan en un dispositivo o emulador con Android. Estas pruebas tienen acceso al marco de Android y a la información de [Instrumentation](https://developer.android.com/reference/android/app/Instrumentation.html), como el [Context](https://developer.android.com/reference/android/content/Context.html) de la aplicación. Puede usar pruebas instrumentadas para pruebas unitarias, pruebas de interfaz de usuario (UI) o pruebas de integración, asegurándose de que los componentes de su aplicación interactúen correctamente con otras aplicaciones. Más comúnmente, se usaa pruebas instrumentales para las pruebas de interfaz de usuario, lo que le permite probar que su aplicación se comporta correctamente cuando un usuario interactúa con su aplicación o ingresa una entrada específica.

Para la mayoría de las formas de prueba de interfaz de usuario, se utiliza el framework *Espresso*, que le permite escribir pruebas de interfaz de usuario automatizadas. 

#### Pruebas unitarias

Las pruebas unitarias deben ser las pruebas fundamentales en su estrategia de prueba de aplicaciones. Al crear y ejecutar pruebas unitarias con su código, puede verificar que la lógica de las áreas o unidades de códigos funcionales individuales es correcta. La ejecución de pruebas unitarias después de cada compilación le ayuda a detectar y solucionar problemas introducidos por cambios de código en su aplicación.

Una prueba de unidad generalmente ejerce la funcionalidad de la unidad de código más pequeña posible (que podría ser un método, clase o componente) de manera repetible. Cree pruebas unitarias cuando necesite verificar la lógica de un código específico en su aplicación. Por ejemplo, si prueba una clase por unidad, su prueba podría verificar que la clase se encuentra en el estado correcto. Para un método, puede probar su comportamiento para diferentes valores de sus parámetros, especialmente focalizando la gestión de valores nulos.

Por lo general, el test unitario se prueba de forma aislada y su prueba monitorea los cambios solo en esa unidad. Puede usar un marco de simulacro como [Mockito](http://mockito.org/) para aislar su unidad de sus dependencias. También puede escribir sus pruebas de unidad para Android en [JUnit4](https://junit.org/junit4/), un marco de prueba de unidad común para código Java.

#### La biblioteca de soporte de pruebas de Android

La biblioteca de compatibilidad de pruebas de Android proporciona la infraestructura y las API para probar aplicaciones de Android, incluida la compatibilidad con JUnit4. Con la biblioteca de compatibilidad de pruebas, puede crear y ejecutar código de prueba para sus aplicaciones.

Es posible que ya tenga instalada la biblioteca de compatibilidad de pruebas de Android con Android Studio. Para verificar el repositorio de soporte de Android, sigue estos pasos:

  1. En Android Studio, seleccione **Tools>Android>SDK Manager**
  2. Haga clic en la pestaña **SDK Tools** y busque el *Support Repository*.
  3. Si es necesario, actualice o instale la libreria.

Las clases de la Biblioteca de compatibilidad de pruebas de Android se encuentran en el paquete *android.support.test*. También hay una API de prueba más antigua en *android.test*. Debe usar las bibliotecas de soporte primero, cuando se le ofrezca una opción entre las bibliotecas de soporte y las API más antiguas, ya que las bibliotecas de soporte ayudan a crear y distribuir pruebas de una manera más limpia y confiable que la codificación directa contra la API en sí.

### <a id="configuracion"></a> Configuración de pruebas

Para preparar un proyecto pary poder probarlo en Android Studio, se debe:

  * Organiza las pruebas en un *source set*.
  * Configurar las dependencias de Gradle de un proyecto para incluir APIs relacionadas con las pruebas.

#### Source set de Android Studio

Los *source set* son colecciones de código en su proyecto que tienen diferentes objetivos de compilación. Cuando Android Studio crea un proyecto, crea tres conjuntos de código fuente para el desarrollador:

  * El conjunto de fuente principal, para el código y los recursos de su aplicación.
    El conjunto de fuentes (test), para las pruebas unitarias de la aplicación. 
    El conjunto de fuentes (androidTest), para pruebas instrumentales de Android. 

Los conjuntos de origen aparecen en el panel de **Project>Android** debajo del nombre del paquete de la aplicación. El conjunto fuente principal incluye solo el nombre del paquete. Los conjuntos de fuente test y androidTest tienen el nombre del paquete seguido de (test) o (androidTest), respectivamente.

![Ubicación de elementos](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/3-2-c-app-testing/source-sets.png)

#### Configurando Gradle para dependencias de prueba

Para usar las API de prueba unitaria, es posible que se deban configurar las dependencias para su proyecto. El archivo de compilación de Gradle predeterminado, proporcionado por las plantillas de actividad, como la plantilla de actividad vacía, incluye algunas de estas dependencias, pero es posible que deba agregar más dependencias para funciones de prueba adicionales, como los frameworks de simulación.

En el archivo build.gradle (Module:app) del proyecto de la aplicación, la siguiente dependencia ya debería estar incluida (si no, debería agregarla):

> testImplementation 'junit:junit:4.12'

Las dependencias de la Prueba de Implementación de Android son necesarias para las pruebas de IU con Espresso, descritas en otro capítulo:

> androidTestImplementation 'com.android.support.test:runner:1.0.1'

> androidTestImplementation 'com.android.support.test.espresso:espresso-core:3.0.1'

Tenga en cuenta que los números de versión de estas bibliotecas pueden haber cambiado. Si Android Studio le informa de una biblioteca más nueva, actualice el número para disponder de la versión actual.

También es posible que desee agregar dependencias para los emparejadores opcionales de Hamcrest y el framework de Mokito:

> testCompile 'org.hamcrest: hamcrest-library:1.3'
> testCompile 'org.mockito: mockito-core:1.10.19'

Después de editar el archivo build.gradle (Module:app), se debe sincronizar el proyecto para continuar. Haga clic en **Sincronizar ahora** en Android Studio cuando se le solicite.

#### Configurando un plan de ejecución de pruebas

Un plan de ejecución de pruebas es una biblioteca o conjunto de herramientas que permite que se realicen las pruebas y que los resultados se impriman en un registro. Un proyecto de Android tiene acceso a un corredor de prueba JUnit básico como parte de las API de JUnit4. La biblioteca de compatibilidad de pruebas de Android incluye un plan de ejecución de pruebas para pruebas instrumentales y de tests Expresso, [AndroidJUnitRunner](https://developer.android.com/reference/android/support/test/runner/AndroidJUnitRunner.html), que también admite JUnit3 y 4.

Este capítulo muestra el plan de ejecución predeterminado para las pruebas unitarias, que se suministra con las plantillas de actividad, como la plantilla de actividad vacía. En el archivo build.gradle (Module:app) del proyecto de una aplicación, el siguiente plan de ejecución ya debería estar incluido en la sección defaultConfig (si no, debería agregarlo):

> testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"

### <a id="creacion"></a>Creación y ejecución de pruebas unitarias.

Se deben crear las pruebas unitarias como un archivo Java genérico utilizando la API de JUnit4 y almacenando las pruebas en el conjunto de archivos fuente (test). Cada plantilla de proyecto de Android Studio incluye este conjunto de test y un archivo de prueba de Java de ejemplo llamado ExampleUnitTest.

#### Creando una nueva clase de prueba

Para crear un nuevo archivo de clase de prueba, agregue un archivo Java al conjunto de fuentes (test) para su proyecto. Los archivos de clase de prueba para la prueba unitaria se denominan normalmente como la clase de la aplicación que se está probando, con "Test" adjunto. Por ejemplo, si tiene una clase llamada Calculator en su aplicación, la clase para sus pruebas unitarias sería CalculatorTest.

Para agregar un nuevo archivo de clase de prueba, siga estos pasos:

  * Expanda la carpeta java y la carpeta para el conjunto de fuentes de prueba de su aplicación. Se muestran los archivos de clase de prueba de unidad existentes.
  * Haga clic con el botón derecho (o presione la tecla Control) en la carpeta del conjunto de fuentes de prueba y seleccione New>JavaClass.
  * Ponga Nombre al archivo y haga clic en Aceptar.

#### Escribiendo tus pruebas

Use la sintaxis y anotaciones de JUnit4 para escribir sus pruebas. Por ejemplo, la clase de prueba que se muestra a continuación incluye las siguientes anotaciones:

  * La anotación @RunWith indica el plan de ejecución de prueba que debe usarse para las pruebas en esta clase.
  * La anotación @SmallTest indica que esta es una prueba pequeña (y rápida).
  * La anotación @Before marca un método como el configurador de la prueba.
  * La anotación @Test marca un método como una prueba real.

Para obtener más información sobre las anotaciones de JUnit, consulte la [Referencia de API de JUnit 4](http://junit.sourceforge.net/javadoc/org/junit/package-summary.html).

    @RunWith(JUnit4.class)
    @SmallTest
    public class CalculatorTest {
        private Calculator mCalculator;
        // Set up the environment for testing
        @Before
        public void setUp() {
            mCalculator = new Calculator();
        }

        // test for simple addition
        @Test
        public void addTwoNumbers() {
            double resultAdd = mCalculator.add(1d, 1d);
            assertThat(resultAdd, is(equalTo(2d)));
        }
    }

El método addTwoNumbers() es la prueba real. La parte clave de una prueba unitaria es la aserción, que se define aquí mediante el método **assertThat()**. Las aserciones son expresiones que deben evaluarse y dar como resultado un valor de verdadero para que la prueba pase. Para obtener más información sobre las aserciones, consulte la documentación de referencia de JUnit para la clase [Assert](http://junit.org/junit4/javadoc/4.12/org/junit/Assert.html).

JUnit 4 proporciona una serie de métodos de aseveración, pero *assertThat()* es el más flexible, ya que permite métodos de comparación de propósito general llamados *matchers*. El framework de Hamcrest se usa comúnmente para los matchers. Hamcrest incluye una gran cantidad de métodos de comparación y permite escribir los propios. Para obtener más información sobre el framework de Hamcrest, consulte la página de inicio de [Java Hamcrest](http://hamcrest.org/JavaHamcrest/).

Tenga en cuenta que el método addTwoNumbers() en este ejemplo incluye solo una aserción. La regla general para las pruebas unitarias es proporcionar un método de prueba separado para cada aseveración individual. Agrupar más de una aserción en un solo método puede hacer que las pruebas sean más difíciles de depurar si solo falla una aserción, y oculta las pruebas que tienen éxito.

#### Ejecutando tus pruebas

Para ejecutar sus pruebas unitarias, siga estos pasos:

  * Para ejecutar una sola prueba, haga clic con el botón derecho (o presione Control y haga clic) sobre ese método de prueba y seleccione **Run**.
  * Para probar todos los métodos en una clase de prueba, haga clic con el botón derecho (o presione Control y haga clic) en el archivo de prueba en el panel de Android>Project y seleccione **Run**.
  * Para ejecutar todas las pruebas en un directorio, haga clic con el botón derecho (o presione Control y haga clic) en el directorio y seleccione **Run Tests**.
  
  ![resultados de pruebas](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/3-2-c-app-testing/run-test-ok.png)

El proyecto se compila, si es necesario, y la vista de prueba aparece en la parte inferior de la pantalla. Si todas las pruebas que ejecutó son exitosas, la barra de progreso en la parte superior de la vista se vuelve verde. Un mensaje de estado en el pie de página también informa "Pruebas aprobadas".


### <a id="practicas"></a>Prácticas relacionadas

La práctica relacionada con los tests de las prácticas unitarias es la [3.2 Tests unitarios](https://codelabs.developers.google.com/codelabs/android-training-unit-tests)

### <a id="aprende"></a>Aprende más

<p>Android Studio documentation:</p>
<ul>
<li><a href="https://developer.android.com/studio/intro/index.html" target="_blank">Android Studio User Guide</a> </li>
<li><a href="https://developer.android.com/studio/debug/am-logcat.html" target="_blank">Write and View Logs</a> </li>
</ul>
<p>Documentación para desarrolladores Android:</p>
<ul>
<li><a href="https://developer.android.com/training/testing/index.html" target="_blank">Buenas prácticas para el Testing</a></li>
<li><a href="https://developer.android.com/training/testing/start/index.html" target="_blank">Empezando con el Testing </a></li>
<li><a href="https://developer.android.com/training/testing/unit-testing/local-unit-tests.html" target="_blank">Construyendo pruebas unitarias</a></li>
</ul>
<p>Otros:</p>
<ul>
<li><a href="http://junit.org/junit4/" target="_blank">JUnit 4 Home Page</a></li>
<li><a href="http://junit.sourceforge.net/javadoc/org/junit/package-summary.html" target="_blank">JUnit 4 API Reference</a></li>
<li><a href="https://www.tutorialspoint.com/java/lang/java_lang_math" target="_blank"><code>java.lang.Math</code></a></li>
<li><a href="http://hamcrest.org/JavaHamcrest/" target="_blank">Java Hamcrest</a></li>
<li><a href="http://mockito.org/" target="_blank">Mockito Home Page</a></li>
<li>Video: <a href="https://www.youtube.com/watch?v=W8LJjfkTKik" target="_blank">Android Testing Support - Patrones de Testeo</a> </li>
<li><a href="https://codelabs.developers.google.com/codelabs/android-testing/index.html" target="_blank">Android Testing Codelab</a></li>
</ul>
