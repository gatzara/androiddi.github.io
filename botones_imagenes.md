# Botones e imágenes clicables
## Contenido:
   [Diseñar para la interactividad.](#disenyo)
   [Botones de diseño](#botones)
   [Respondiendo a los eventos de clic de botón](#eventos)
   [Usando imágenes clicables](#imagenes)
   [Usando un botón de acción flotante](#fab)
   [Reconociendo gestos](#gestos)
   [Práctica relacionada](#practica)
   [Aprende más](#aprende)

### <a id="disenyo"></a>Diseñar para la interactividad.

La interfaz de usuario (IU) que aparece en la pantalla de un dispositivo con Android consiste en una jerarquía de objetos llamados vistas. Cada elemento de la pantalla es una vista.

La clase *View* representa el componente básico para todos los componentes de la interfaz de usuario. *View* es la clase base para las clases que proporcionan componentes de IU interactivos, como los elementos *Button*. Los usuarios tocan estos elementos en una pantalla táctil o hacen clic en ellos con un dispositivo señalador. Cualquier elemento que los usuarios toquen o hagan clic para realizar una acción se llama elemento seleccionable.

Para una aplicación de Android, la interacción del usuario generalmente implica tocar, escribir, usar gestos o hablar. El famewrok de Android proporciona elementos correspondientes de la interfaz de usuario (IU), como botones, imágenes accesibles, menús, teclados, campos de entrada de texto y un micrófono.

Al diseñar una aplicación interactiva, asegúrese de que la aplicación sea intuitiva; es decir, la aplicación debería funcionar como lo esperan los usuarios. Por ejemplo, cuando se alquila un automóvil, se debe esperar que el volante, el cambio de marchas, los faros e indicadores estén en un lugar determinado. Otro ejemplo es que cuando entras en una habitación por primera vez, esperas que el interruptor de luz esté en un lugar determinado. De manera similar, cuando un usuario inicia una aplicación, el usuario espera que se puedan hacer clic en los botones e imágenes. No se deben ignorar las expectativas establecidas, o se dificultará el uso de la app por parte de los usuarios.

Nota: los usuarios de Android esperan que los elementos de la interfaz de usuario actúen de ciertas maneras, por lo que es importante que su aplicación sea coherente con otras aplicaciones de Android. Para satisfacer a sus usuarios, cree un diseño que les brinde opciones predecibles.

### <a id="botones"></a> Botones de diseño

A la gente le gusta presionar botones. Muéstrele a alguien un gran botón rojo con un mensaje que dice "No presionar" y la persona probablemente presionará el botón, solo por el placer de presionar un gran botón rojo. (Que el botón esté prohibido también es un factor).

Usas la clase **Button** para hacer un botón para una aplicación de Android. Los botones pueden tener el siguiente diseño:

  * Solo texto, como se muestra en el lado izquierdo de la figura a continuación.
  * Solo icono, como se muestra en el centro de la figura a continuación.
  * Tanto el texto como un icono, como se muestra en el lado derecho de la figura a continuación.
  
  ![botones](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/4-1-c-buttons-and-clickable-images/dg_button-types.png)
  
 Cuando el usuario toca o hace clic en un botón, el botón realiza una acción. El texto o el icono del botón debe proporcionar una pista sobre cuál será esa acción. (Los botones a veces se llaman "botones pulsadores" en la documentación de Android).

Un botón suele ser un rectángulo o un rectángulo redondeado con un título o icono descriptivo en su centro. Los elementos del **Button** de Android siguen las pautas de la especificación de Material Design de Android. (Aprende más sobre Diseño de materiales en otra lección).

Android ofrece varios tipos de elementos de botón, incluidos los botones en relieve y los botones planos, como se muestra en la siguiente figura. Cada botón tiene tres estados: normal, deshabilitado y presionado.

![tipos de botones](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/4-1-c-buttons-and-clickable-images/dg_button_types_composite.png)

En la figura de arriba:
  * Botón elevado en tres estados: normal, deshabilitado y presionado
  * Botón plano en tres estados: normal, deshabilitado y presionado

#### Diseño de botones elevados

Un botón elevado es un rectángulo delineado o redondeado que aparece levantado de la pantalla; el sombreado a su alrededor indica que es posible tocarlo o hacer clic en él. El botón elevado puede mostrar texto, un icono o ambos.

Para usar botones elevados que cumplan con la especificación de Material Desgin, siga estos pasos:

  * Incluya en el archivo build.gradle (Module:app) la biblioteca android.support:appcompat-v7, si no lo está ya:

    > implementation 'com.android.support:appcompat-v7:28.0.0.'

 En el fragmento de código anterior, 28.0.0 es el número de versión. Si el número de versión que especificó es inferior al número de versión de biblioteca disponible actualmente, Android Studio le avisará ("hay una versión más reciente disponible"). Actualice el número de versión al que Android Studio le indique que use.

  * Haga que su actividad extienda android.support.v7.app.AppCompatActivity:

     > public class MainActivity extends AppCompatActivity {
     >    // ...
     > }
     
  * Utilice el elemento **Button** en el archivo de layout. Un botón elevado es el estilo por defecto.

     > <Button
     >    android:layout_width = "wrap_content"
     >    android:layout_height = "wrap_content"
     >    <! - más atributos ... ->
     > />

Utilice los elementos de botón levantados para dar más importancia a las acciones en diseños con una gran cantidad de contenido variable. Un botón elevado agrega dimensión a un diseño plano: muestra una sombra de fondo cuando se toca (presiona) o se hace clic, como se muestra a continuación.

![estados del boton](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/4-1-c-buttons-and-clickable-images/dg_button_raised_composite.png)
