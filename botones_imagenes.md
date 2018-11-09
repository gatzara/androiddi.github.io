# Botones e imágenes clicables
## Contenido:
  * [Diseñar para la interactividad.](#disenyo)
  * [Botones de diseño](#botones)
  * [Respondiendo a los eventos de clic de botón](#eventos)
  * [Usando imágenes clicables](#imagenes)
  * [Usando un botón de acción flotante](#fab)
  * [Reconociendo gestos](#gestos)
  * [Práctica relacionada](#practica)
  * [Aprende más](#aprende)

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

  1 Incluya en el archivo build.gradle (Module:app) la biblioteca android.support:appcompat-v7, si no lo está ya:

    > implementation 'com.android.support:appcompat-v7:28.0.0.'

 En el fragmento de código anterior, 28.0.0 es el número de versión. Si el número de versión que especificó es inferior al número de versión de biblioteca disponible actualmente, Android Studio le avisará ("hay una versión más reciente disponible"). Actualice el número de versión al que Android Studio le indique que use.

  2 Haga que su actividad extienda android.support.v7.app.AppCompatActivity:

     > public class MainActivity extends AppCompatActivity {
     >    // ...
     > }
     
  3 Utilice el elemento **Button** en el archivo de layout. Un botón elevado es el estilo por defecto.

     > <Button
     >    android:layout_width = "wrap_content"
     >    android:layout_height = "wrap_content"
     >    <! - más atributos ... ->
     > />

Utilice los elementos de botón levantados para dar más importancia a las acciones en diseños con una gran cantidad de contenido variable. Un botón elevado agrega dimensión a un diseño plano: muestra una sombra de fondo cuando se toca (presiona) o se hace clic, como se muestra a continuación.

![estados del boton](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/4-1-c-buttons-and-clickable-images/dg_button_raised_composite.png)

En la figura de arriba:

  * Estado normal: Un botón elevado.
  * Estado deshabilitado: cuando está deshabilitado, el botón está atenuado y no está activo en el contexto de la aplicación. En la mayoría de los casos, ocultaría un botón inactivo, pero puede haber ocasiones en las que quiera mostrarlo como desactivado.
  * Estado presionado: el estado presionado, con una sombra de fondo más grande, indica que se está tocando o haciendo clic en el botón. Cuando adjunta una devolución de llamada al botón (como el atributo android:onClick), se llama a la devolución de llamada cuando el botón está en este estado.

#### Creando un botón elevado con texto.

Algunos elementos de botón elevados se diseñan mejor como texto, sin un icono, como el botón Guardar, ya que un icono por sí solo puede no transmitir un significado obvio. La clase Button amplía la clase TextView. Para usarlo, agréguelo al diseño XML:

> <Button
>    android:layout_width = "wrap_content"
>    android:layout_height = "wrap_content"
>    android:text = "@ string/button_text"
>    <! - más atributos ... ->
> />

La mejor práctica con un botón de texto es definir una palabra muy corta como un recurso de cadena (*button_text* en el ejemplo anterior), para que la cadena se pueda traducir. Por ejemplo, **Guardar** podría traducirse al francés como **Enregistrer** sin cambiar ninguno de los códigos.

#### Creando un botón elevado con un icono y texto.

Mientras que un botón normalmente muestra texto que le dice al usuario cuál es la acción, un botón elevado también puede mostrar un icono junto con el texto.

##### Elegir un icono

Para elegir imágenes de un ícono estándar cuyo tamaño se modifique para diferentes pantallas, siga estos pasos:

  1. Expanda app>res en el panel Project> Android, y haga clic con el botón derecho en la carpeta **drawable**.
  2. Seleccione **New> Image Asset**. Aparece el cuadro de diálogo de configuración del Asset.
  
  ![creando asset](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/4-1-c-buttons-and-clickable-images/as_configure_image_asset_01.png)
  
  3. Elija la  **Action Bar and Tab Icons** en el menú desplegable. (Para obtener una descripción completa de este cuadro de diálogo, consulte Crear íconos de aplicaciones con Image Asset Studio).
  4. Haga clic en **ClipArt**: imagen (el logotipo de Android) para seleccionar una imagen prediseñada como icono. Aparece una página de iconos como se muestra a continuación. Haga clic en el icono que desea utilizar.
  
  ![clipart de boton](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/4-1-c-buttons-and-clickable-images/as_configure_image_asset_02.png)
  
  5. Opcional: elija HOLO_DARK como **Tema** para configurar el ícono para que sea blanco sobre un fondo de color oscuro o negro.
  6. Opcional: Dependiendo de la forma del ícono, es posible que desee agregar relleno al ícono para que el ícono no se amontone en el texto. Arrastre el control deslizante Relleno hacia la derecha para agregar más relleno.
  7. Haga clic en Siguiente y luego haga clic en Finalizar en el cuadro de diálogo *Confirm Icon Path*. El nombre del icono debería aparecer ahora en la carpeta app>res>drawable.

Las imágenes vectoriales de un icono estándar se redimensionan automáticamente para diferentes tamaños de pantallas de dispositivos. Para elegir imágenes vectoriales, sigue estos pasos:

  1. Expanda **app>res** en el panel Project>Android, y haga clic con el botón derecho en la carpeta **drawable**.
  2. Elija **New>Vector Asset** para un icono que se redimensiona automáticamente para cada pantalla.
  3. El cuadro de diálogo **Vector Asset Studio** aparece para un vector activo. Haga clic en el botón de opción **Material Icon** y luego haga clic en el botón Elegir para elegir un icono de la especificación de **Material Design**. (Para obtener una descripción completa de este cuadro de diálogo, consulte Agregar gráficos vectoriales de densidad múltiple).
  4. Haga clic en Siguiente después de elegir un icono y haga clic en Finalizar para finalizar. El nombre del icono debería aparecer ahora en la carpeta app>res>drawable.

#### Añadiendo el botón con texto e icono al diseño.

Para crear un botón con texto y un ícono como se muestra en la figura a continuación, use un Button en su diseño XML. Agregue el atributo *android:drawableLeft* para dibujar el icono a la izquierda del texto del botón, como se muestra en la siguiente figura:

> <Button
>    android:layout_width="wrap_content"
>    android:layout_height="wrap_content"
>    android:text="@string/button_text"
>    android:drawableLeft="@drawable/button_icon"
>    <!-- more attributes ... -->
> />

![Botón con icono y texto](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/4-1-c-buttons-and-clickable-images/alert_with_icon_raised_button.png)

Creando un botón levantado con solo un icono

Si el ícono se entiende universalmente, es posible que desee usarlo en lugar de texto.

Para crear un botón elevado con solo un icono o una imagen (sin texto), use la clase ImageButton, que extiende la clase ImageView. Puede agregar un ImageButton a su diseño XML de la siguiente manera:

<ImageButton
    android: layout_width = "wrap_content"
    android: layout_height = "wrap_content"
    android: src = "@ drawable / button_icon"
    <! - más atributos ... ->
/>

#### Cambiando el estilo y apariencia de los botones elevados.

La forma más sencilla de mostrar un botón elevado más prominente es usar un color de fondo diferente para el botón. Puede especificar el atributo android:background con un recurso drawable o de color:

> android:background="@color/colorPrimary"

La apariencia de un botón, el color de fondo y la fuente, puede variar de un dispositivo a otro, porque los dispositivos de diferentes fabricantes a menudo tienen diferentes estilos predeterminados para los controles de entrada. Puede controlar exactamente el estilo de sus botones y otros controles de entrada utilizando un tema que aplique a toda su aplicación.

Por ejemplo, para asegurarse de que todos los dispositivos que pueden ejecutar el tema Holo usarán el tema Holo para su aplicación, declare lo siguiente en el elemento <aplicación> del archivo AndroidManifest.xml:

> android:theme ="@android:style/Theme.Holo"

Después de agregar la declaración anterior, la aplicación se mostrará usando el tema.

Las aplicaciones diseñadas para Android 4.0 y superiores también pueden usar la familia de temas públicos **DeviceDefault**. Los temas de DeviceDefault son alias para el aspecto y estilo nativos del dispositivo. La familia de temas DeviceDefault y la familia de estilo de widgets ofrecen formas para que los desarrolladores seleccionen el tema nativo del dispositivo con todas las personalizaciones intactas.

Para las aplicaciones de Android que se ejecutan en 4.0 y posteriores, tiene las siguientes opciones:

  * Use un tema, como uno de los temas de Holo, para que su aplicación tenga exactamente el mismo aspecto en todos los dispositivos con Android que ejecuten 4.0 o más nuevos. En este caso, el aspecto de la aplicación no cambia cuando se ejecuta en un dispositivo con un aspecto predeterminado diferente o un aspecto personalizado.
  * Use uno de los temas de DeviceDefault para que su aplicación adquiera el aspecto de la máscara predeterminada del dispositivo.
  No utilice un tema bajo riesgod de tener resultados impredecibles en algunos dispositivos.

#### Diseño de botones planos

Un botón plano, también conocido como botón de texto o botón sin bordes, es un botón de solo texto que se ve plano y no tiene una sombra. La principal ventaja de los botones planos es la simplicidad: un botón plano no distrae al usuario del contenido principal tanto como lo hace un botón elevado. Los botones planos son útiles para los diálogos que requieren la interacción del usuario, como se muestra en la siguiente figura. En este caso, se desea que el botón use la misma fuente y el mismo estilo que el texto circundante para mantener una apariencia coherente en todos los elementos del cuadro de diálogo.

### <a id="practica"></a>Contenido práctico
p>TLa práctica relacionada con el tema es <a href="https://codelabs.developers.google.com/codelabs/android-training-clickable-images" target="_blank">4.1: Clickable images</a>.</p>
### <a id="aprende"></a>Aprende más
<p>Documentación Android Studio:</p>
<ul>
<li><a href="https://developer.android.com/studio/intro/index.html" target="_blank">Guía de Usuario deAndroid Studio</a> </li>
<li><a href="http://developer.android.com/tools/help/image-asset-studio.html" target="_blank">Crear iconos con Image Asset Studio</a></li>
</ul>
<p>Documentación de desarrolladores de Android:</p>
<ul>
<li><a href="https://developer.android.com/guide/topics/ui/" target="_blank">User interface &amp; navigation</a>  </li>
<li><a href="https://developer.android.com/studio/write/layout-editor.html" target="_blank">Build a UI with Layout Editor</a></li>
<li><a href="https://developer.android.com/training/constraint-layout/index.html" target="_blank">Build a Responsive UI with <code>ConstraintLayout</code></a></li>
<li><a href="http://developer.android.com/guide/topics/ui/declaring-layout.html" target="_blank">Layouts</a></li>
<li><a href="http://developer.android.com/reference/android/view/View.html" target="_blank"><code>View</code></a></li>
<li><a href="http://developer.android.com/reference/android/widget/Button.html" target="_blank"><code>Button</code></a></li>
<li><a href="https://developer.android.com/reference/android/widget/ImageView.html" target="_blank"><code>ImageView</code></a></li>
<li><a href="http://developer.android.com/reference/android/widget/TextView.html" target="_blank"><code>TextView</code></a></li>
<li><a href="https://developer.android.com/guide/topics/ui/controls/button.html" target="_blank">Buttons</a></li>
<li><a href="https://developer.android.com/guide/topics/ui/ui-events.html" target="_blank">Input events overview</a></li>
<li><a href="http://developer.android.com/guide/topics/ui/themes.html" target="_blank">Styles and themes</a></li>
<li><a href="https://developer.android.com/training/gestures/index.html" target="_blank">Use touch gestures</a></li>
</ul>
<p>Material Design spec:</p>
<ul>
<li><a href="https://material.google.com/components/buttons.html" target="_blank">Components - Buttons</a></li>
<li><a href="https://material.io/design/interaction/gestures.html" target="_blank">Gestures design guide</a></li>
</ul>
<p>Other: </p>
<ul>
<li>Codelabs: <a href="https://codelabs.developers.google.com/codelabs/constraint-layout/index.html" target="_blank">Using <code>ConstraintLayout</code> to design your views</a></li>
<li>Android Developers Blog: <a href="http://android-developers.blogspot.com/2012/01/holo-everywhere.html" target="_blank">Holo Everywhere</a></li>
<li>Developer blog: <a href="http://android-developers.blogspot.com/2014/10/implementing-material-design-in-your.html" target="_blank">Implementing Material Design in Your Android app</a></li>
</ul>
