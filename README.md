# androiddi.github.io
Apartat d'Android en el mòdul de DI de DAM

## Construyendo la primera app

### Layouts y recursos para la interfaz de usuario

Contenido:
* [Puntos de vista](#puntos)
* [El editor de diseño](#editor)
* [Editando XML directamente](#editando)
* [Archivos de recursos](#archivos)
* [Respondiendo a los gestos](#respondiendo)
* [Practicas relacionadas](#practicas)
* [Aprende más](#aprende)

Este capítulo describe el diseño de la interfaz de usuario (UI) de la pantalla y otros recursos que crea para la aplicación, y el código que usaría para responder a la interacción de un elemento de UI de un usuario.

#### <a id="puntos"></a> Puntos de vista

La interfaz de usuario consta de una jerarquía de objetos llamados vistas: cada elemento de la pantalla es una vista. La clase Vista representa el bloque de construcción básico para todos los componentes de la interfaz de usuario y la clase base para las clases que proporcionan componentes de la interfaz de usuario interactivos, como botones, casillas de verificación o campos de entrada de texto.

Una vista tiene una ubicación, expresada como un par de coordenadas izquierda y superior, y dos dimensiones, expresadas como un ancho y una altura. La unidad de ubicación y dimensiones es el píxel independiente de densidad (dp).

El sistema Android proporciona cientos de subclases de vista predefinidas. Las subclases de vista de uso común descritas en las siguientes lecciones incluyen:

  * [TextView](http://developer.android.com/reference/android/widget/TextView.html) para mostrar texto
  * [EditText](http://developer.android.com/reference/android/widget/EditText.html) para permitir al usuario introducir y editar texto
  * [Botón](http://developer.android.com/reference/android/widget/Button.html) y otros elementos seleccionables (como [RadioButton](http://developer.android.com/reference/android/widget/RadioButton.html), [CheckBox](http://developer.android.com/reference/android/widget/CheckBox.html) y [Spinner](http://developer.android.com/reference/android/widget/Spinner.html)) para ofrecer un comportamiento interactivo
  * [ScrollView](http://developer.android.com/reference/android/widget/ScrollView.html) y [RecyclerView](https://developer.android.com/reference/android/support/v7/widget/RecyclerView.html) para mostrar elementos desplazables
  * [ImageView](http://developer.android.com/reference/android/widget/ImageView.html) para mostrar imágenes
  * [ConstraintLayout](https://developer.android.com/reference/android/support/constraint/ConstraintLayout.html), [RelativeLayout](https://developer.android.com/reference/android/widget/RelativeLayout.html) y [LinearLayout](https://developer.android.com/reference/android/widget/LinearLayout.html) para contener otras vistas y colocarlas

Se puede definir una *View* para que aparezca en la pantalla y responder a un gesto de usuario. También se puede definir una *View* para aceptar la introducción de texto o para que sea invisible hasta que sea necesario.

A su vez, se puede especificar Ver elementos en archivos de recursos de diseño. Los recursos de diseño se escriben en XML y se encuentran en la carpeta **layout** dentro de la carpeta **res** en el panel **Project> Android.**

##### Grupos ViewGroup

Los elementos *View* se pueden agrupar dentro de un [ViewGroup](https://developer.android.com/reference/android/view/ViewGroup.html), que actúa como un contenedor. La relación es padre-hijo, en la que el padre es un *ViewGroup* y el hijo es una vista u otro *ViewGroup*. Los siguientes son grupos de ViewGroup comúnmente usados:

  * [ConstraintLayout](https://developer.android.com/reference/android/support/constraint/ConstraintLayout.html): grupo que coloca los elementos de la IU (elementos de la vista secundaria) mediante el uso de conexiones restringidas a otros elementos y a los bordes del diseño (vista principal).
  * [ScrollView](https://developer.android.com/reference/android/widget/ScrollView.html): un grupo que contiene otro elemento de vista secundario y habilita el desplazamiento del elemento de vista secundario.
  * [RecyclerView](https://developer.android.com/reference/android/widget/RecyclerView.html): un grupo que contiene una lista de otros elementos de *View* o grupos de *ViewGroup* y permite desplazarlos agregando y eliminando elementos de tipo *View* inámicamente de la pantalla.

##### Distribución de los grupos ViewGroup

Los elementos de vista para una pantalla están organizados en una jerarquía. En la raíz de esta jerarquía se encuentra un *ViewGroup* que contiene el diseño de toda la pantalla. *ViewGroup* puede contener elementos de vista secundarios u otros grupos de tipo *ViewGroup* como se muestra en la siguiente figura:

![Jerarquía ViewGroup](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/1-2-c-layouts-and-resources-for-the-ui/dg_viewgroup_hierarchy.png)

En la figura de arriba:

1. El *ViewGroup* raíz.
2. El primer conjunto de elementos *View* secundarios y *ViewGroup* cuyo padre es la raíz.

Algunos grupos de *ViewGroup* se designan como layouts porque organizan elementos *View* secundarios de una manera específica y se utilizan normalmente como el *ViewGroup* raíz. Algunos ejemplos de diseños son:

  * [ConstraintLayout](http://tools.android.com/tech-docs/layout-editor): un grupo de elementos secundarios *View* elementos que utilizan restricciones, bordes y pautas para controlar cómo se colocan los elementos en relación con otros elementos en el diseño. ConstraintLayout fue diseñado para que sea fácil hacer clic y arrastrar elementos *View* en el editor de diseño.
  * [LinearLayout](https://developer.android.com/reference/android/widget/LinearLayout.html): un grupo de elementos secundarios de clase *View* y que se posicionan horizontalmente o verticalmente.
  * [RelativeLayout](https://developer.android.com/reference/android/widget/RelativeLayout.html): un grupo de elementos secundarios de clase *View* en el que cada elemento está posicionado y alineado con respecto a otros elementos dentro del *ViewGroup*. En otras palabras, las posiciones de los elementos de vista secundarios pueden describirse entre sí o con el grupo de vista principal.
  * [TableLayout](https://developer.android.com/reference/android/widget/TableLayout.html): un grupo de elementos de vista secundarios organizados en filas y columnas.
  * [FrameLayout](https://developer.android.com/reference/android/widget/FrameLayout.html): un grupo de elementos secundarios de tipo *View* en una pila. FrameLayout está diseñado para bloquear un área en la pantalla para mostrar una vista. Los elementos de hijos de clase *View* se dibujan en una pila, con el hijo agregado más recientemente en la parte superior. El tamaño del FrameLayout es el tamaño de su elemento hijo *View* más grande.
  * [GridLayout](https://developer.android.com/reference/android/widget/GridLayout.html): grupo que coloca sus elementos *View* secundarios en una cuadrícula rectangular que se puede desplazar.
  
  ![Diferentes tipos de layouts](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/1-2-c-layouts-and-resources-for-the-ui/dg_common_layouts_visual_rep.png)
  
 A continuación se muestra un ejemplo simple de un elemento *LinearLayout* con elementos secundarios *View* especificados en el fichero de diseño (activity_main.xml), junto con un diagrama jerárquico y una captura de pantalla del diseño final real 
 
 ![Vista del LinearLayout](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/1-2-c-layouts-and-resources-for-the-ui/dg_layout_diagram_and_hierarchy.png)
 
 En la figura de arriba:

 1. LinearLayout, el grupo de vista raíz, contiene todos los elementos de vista secundarios en una orientación vertical.
 2. Botón (button_toast). El primer elemento secundario de Vista aparece en la parte superior en LinearLayout.
 3. TextView (show_count). El segundo elemento secundario de vista aparece debajo del primer elemento secundario de vista en LinearLayout.
 4. Botón (button_count). El tercer elemento de vista secundario aparece debajo del segundo elemento de vista secundario en LinearLayout.

La jerarquía de diseño puede volverse compleja para una aplicación que muestra muchos elementos de Vista en una pantalla. Es importante entender la jerarquía, ya que afecta si los elementos de Vista son visibles y cuán eficientemente se dibujan.

Sugerencia: Puede explorar la jerarquía de diseño de su aplicación utilizando el [Hierarchy Viewer](https://developer.android.com/studio/profile/hierarchy-viewer-walkthru.html). Muestra una vista de árbol de la jerarquía y permite analizar el rendimiento de los elementos de vista en un dispositivo con Android. Los problemas de rendimiento se tratan posteriormente.
    
#### <a id="editor"></a> Editor de diseño

Se definen los layouts en el editor de diseños, o directamente introduciendo el código XML.

El editor de diseño muestra una representación visual de código XML. Puede arrastrar los elementos de clase *View* al panel de diseño y organizar, redimensionar y especificar atributos para ellos. Inmediatamente se ve el efecto de los cambios que se realizan.

Para usar el editor de diseño, haga doble clic en el archivo de diseño XML (activity_main.xml). El editor de diseño aparece con la pestaña Diseño en la parte inferior resaltada. (Si la pestaña Texto está resaltada y se ve el código XML, haga clic en la pestaña Diseño). Para la plantilla Actividad vacía, el diseño es como se muestra en la siguiente figura.

![Editor de diseño](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/1-2-c-layouts-and-resources-for-the-ui/as_activity_main_in_project_pane_annot.png)

1. Fichero de diseño XML (**activity_main.xml**).
2. Pestañas de **diseño** y de **texto**. Haga clic en Diseño para ver el editor de diseño o Texto para ver el código XML.
3. Panel de la **paleta**. El panel Paleta proporciona una lista de elementos y diseños de la interfaz de usuario. Agregue un elemento o diseño a la interfaz de usuario arrastrándolo al panel de diseño.
4. **Árbol de componentes**. El panel Árbol de componentes muestra la jerarquía de diseño. Haga clic en un elemento *View* o *ViewGroup* en este panel para seleccionarlo. Los elementos *View* se organizan en una jerarquía de árbol de padres e hijos, en la que un hijo hereda los atributos de su padre. En la figura anterior, *TextView* es un elemento secundario de *ConstraintLayout*.
5. Paneles de diseño y planos. Arrastre los elementos *View* desde el panel Paleta al panel de diseño o plano para colocarlos en el layout. En la figura de arriba, el diseño muestra solo un elemento: un *TextView* que muestra "Hello World".
6. Pestaña de **Atributos**. Haga clic en Atributos para mostrar el panel Atributos para configurar atributos para un elemento *Vista*.

##### Barras de herramientas del editor de layout

Las barras de herramientas del editor de layout proporcionan botones para configurar su diseño y cambiar su apariencia. La barra de herramientas superior le permite configurar la apariencia de la vista previa del diseño en el editor de diseño:

![Barra de herramientas del editor de layout](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/1-2-c-layouts-and-resources-for-the-ui/as_constraint_toolbar1_annot.png)

La figura de arriba muestra la barra de herramientas superior del editor de layout:

1. Seleccionar **superficie de layout**: seleccione **Diseño** para mostrar una vista previa en color de los elementos de la interfaz de usuario en su diseño, o **Plano** para mostrar solo los contornos de los elementos. Para ver ambos paneles, de lado a lado, seleccione **Diseño + Plano**.
2. **Orientación en el Editor**: seleccione **Vertical** u **Horizontal** para mostrar la vista previa en una orientación vertical u horizontal. La configuración de orientación permite previsualizar las orientaciones de diseño sin ejecutar la aplicación en un emulador o dispositivo. Para crear diseños alternativos, seleccione **Crear variación apaisada** u otras variaciones.
3. **Dispositivo en el Editor**: seleccione el tipo de dispositivo (teléfono/tablet, Android TV o Android Wear).
4. **Versión de la API en el Editor**: seleccione la versión de Android que se usará para mostrar la vista previa.
5. **Tema en el Editor**: seleccione un tema (como **AppTheme**) para aplicar a la vista previa.
6. **Configuración regional en Editor**: seleccione el idioma y la configuración regional para la vista previa. Esta lista muestra solo los idiomas disponibles en los recursos de cadena (consulte la lección sobre localización para obtener detalles sobre cómo agregar idiomas). También puede seleccionar **Vista previa de derecha a izquierda** para ver el diseño como si se hubiera elegido un idioma RTL.

El editor de diseño también ofrece una segunda barra de herramientas que le permite configurar la apariencia de los elementos de la interfaz de usuario en un *ConstraintLayout* y acercar y alejar la vista previa:

![Barra de herramienta secundaria de diseño de layout](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/1-2-c-layouts-and-resources-for-the-ui/as_constraint_toolbar2_annot.png)

La figura de arriba muestra la barra de herramientas de edición ConstraintLayout:

1. **Mostrar**: seleccione **Mostrar restricciones** y **Mostrar márgenes** para mostrarlos en la vista previa o para dejar de mostrarlos.
2. **Conectar automáticamente**: habilite o inhabilite la conexión automática. Con **Autoconnect** habilitado, puede arrastrar cualquier elemento (como un botón) a cualquier parte de un diseño para generar restricciones dentro del diseño principal.
3. **Borrar todas las restricciones**: Borre todas las restricciones en todo el diseño.
4. **Inferir restricciones**: crear restricciones por inferencia.
5. **Márgenes predeterminados**: establece los márgenes predeterminados.
6. **Pack**: Empaquetar o expandir los elementos seleccionados.
7. **Alinear**: alinear los elementos seleccionados.
8. **Pautas**: Añadir pautas verticales u horizontales.
9. **Controles de zoom**: acercar o alejar.

##### Usando el ConstraintLayout
El editor de diseño ofrece más funciones en la pestaña **Diseño** cuando usa *ConstraintLayout*, incluidos los controles para definir restricciones.

Una restricción es una conexión o alineación con otro elemento de la interfaz de usuario, con el diseño principal o con una directriz invisible. Cada restricción aparece como una línea que se extiende desde un controlador circular. Después de seleccionar un elemento de la interfaz de usuario en el panel **Árbol de componentes** o hacer clic en él en el editor de diseño, el elemento muestra un controlador de cambio de tamaño en cada esquina y un control de restricción circular en el centro de cada lado.

![Restricciones en el ConstraintLayout](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/1-2-c-layouts-and-resources-for-the-ui/as_layout_constraint_2_handles_annot.png)

La figura anterior muestra los controles de restricción y cambio de tamaño en los elementos de vista en un diseño:

1. **Cambiar el tamaño de la selección.**
2. **Línea de restricción y elemento seleccionado**. En la figura, la restricción alinea el lado izquierdo del botón Toast con el lado izquierdo del diseño.
3. **Control de restricción sin una línea de restricción**.
4. **Línea de base del elemento seleccionado**. El controlador de línea base alinea la línea base de texto de un elemento con la línea base de texto de otro elemento.

En los paneles de planos o de diseño, los siguientes controladores aparecen en el elemento TextView:

  * **Control de restricción**: para crear una restricción, haga clic en el control de restricción, que se muestra como un círculo en cada lado de un elemento. Luego arrastre el círculo a otro controlador de restricción o a un límite principal. Una línea en zigzag representa la restricción.
  
  ![Control de restricción](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/1-2-c-layouts-and-resources-for-the-ui/handles.png)
  
  * **Control de redimensionamiento**: Se pueden arrastrar los controles cuadrados de tamaño para cambiar el tamaño del elemento. Mientras se arrastra, el controlador cambia a una esquina en ángulo.
  
    ![Control de redimensionamiento](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/1-2-c-layouts-and-resources-for-the-ui/handle_resize.png)
  
Se pueden arrastrar los controladores de cambio de tamaño en cada esquina del elemento de la interfaz de usuario para cambiar el tamaño, pero al hacerlo se deben codificar las dimensiones de anchura y altura, lo que se debería evitar para la mayoría de los elementos porque las dimensiones codificadas no se adaptan a diferentes densidades de pantalla.

#### <a id="editando"></a> Editando el archivo XML directamente
#### <a id="archivos"></a> Archivos de recursos
#### <a id="respondiendo"></a> Respondiendo a los gestos
#### <a id="practicas"></a> Prácticas relacionadas
#### <a id="aprende"></a> Aprende más
