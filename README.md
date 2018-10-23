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

##### Creando restricciones a un elemento de la interfaz gráfica

Para agregar una restricción a un elemento de la interfaz de usuario, haga clic en el controlador circular y arrastre una línea a otro elemento o a un lado del layout, como se muestra en las dos figuras animadas a continuación. Para eliminar una restricción de un elemento, haga clic en el controlador circular.

![Creando restricciones usando ConstraintLayout](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/1-2-c-layouts-and-resources-for-the-ui/hello_world_textview_constraints.gif)

![Más restricciones entre elementos](https://drive.google.com/open?id=1jKdsaoaidrMgId4vJ4T5TBPpH9ixMmB8)

Las restricciones que se definen en el editor de diseño se crean como atributos XML, que se pueden ver en la pestaña **Texto** como se describe en "Editar XML directamente" en este capítulo. Por ejemplo, el siguiente código XML se crea restringiendo la parte superior de un elemento a la parte superior de su padre:

> app:layout_constraintTop_toTopOf="parent"

##### Creando una restricción de linea de base

Puede alinear un elemento de la interfaz de usuario que contenga texto, como *TextView* o *Button* con otro elemento de la interfaz de usuario que contenga texto. Una restricción de línea de base le permite restringir los elementos para que coincidan las líneas de base del texto. Seleccione el elemento de la interfaz de usuario que tiene texto y luego desplace el puntero sobre el elemento hasta que aparezca el botón de restricción ![botón de línea de base](https://drive.google.com/open?id=10txOg0bstvVnmc0VNzEPWyGW5_SekdWQ) de línea de base debajo del elemento.

Haga clic en el botón de restricción de línea de base. El control de línea de base aparece, parpadeando en verde como se muestra en la figura animada. Arrastre una línea de restricción de línea de base a la línea de base del otro elemento de la interfaz de usuario. Puede verlo en la pestaña Texto como se describe en "Editar XML directamente" en este capítulo. Por ejemplo, el siguiente código XML se crea restringiendo la parte superior de un elemento a la parte superior de su padre:

![Restricción de linea de base](https://drive.google.com/open?id=1NdPNOlm592-TqZgn4XqKPh9ToI_ezeKm)

##### Usando el panel de atributos

El panel **Atributos** ofrece acceso a todos los **Atributos** XML que puede asignar a un elemento de la interfaz de usuario. Se pueden encontrar los **Atributos** (conocidos como propiedades) comunes a todas las vistas en la documentación de la clase Ver.

Para mostrar el panel **Atributos**, haga clic en la pestaña **Atributos** en el lado derecho del editor de diseño. El panel **Atributos** incluye un panel de tamaño cuadrado denominado *inspector de vista*. Los símbolos dentro del inspector de vista representan los ajustes de altura y anchura.

![Panel de atributos](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/1-2-c-layouts-and-resources-for-the-ui/as_layout_width_height_box_annot.png)

La figura de arriba muestra el panel de atributos:

1. **Control de tamaño de vista vertical**. El control de tamaño vertical, que aparece en la parte superior e inferior del inspector de vista, especifica la propiedad *layout_height*. Los ángulos indican que este control de tamaño se establece en wrap_content, lo que significa que el elemento UI se expande verticalmente según sea necesario para ajustarse a su contenido. El "8" indica un margen estándar establecido en 8 dp.
2. **Control de tamaño de vista horizontal**. El control de tamaño horizontal, que aparece a la izquierda y a la derecha del inspector de vista, especifica el *layout_width*. Los ángulos indican que este control de tamaño se establece en wrap_content, lo que significa que el elemento UI se expande horizontalmente según sea necesario para ajustarse a su contenido, hasta un margen de 8 dp.
3. ** Botón de cerrar del Panel de atributos**. Haga clic para cerrar el panel.

Los atributos layout_width y layout_height en el panel Atributos cambian a medida que cambia los controles de tamaño horizontal y vertical del inspector. Estos atributos pueden tomar uno de los tres valores para un ConstraintLayout:

  * La configuración **match_constraint** expande el elemento UI para rellenar su padre por ancho o alto hasta un margen, si se establece ese margen. El padre en este caso es el ConstraintLayout.
  * La configuración de **wrap_content** reduce el elemento de la IU al tamaño de su contenido. Si no hay contenido, el elemento se vuelve invisible.
  * Para especificar un tamaño fijo ajustado para el tamaño de la pantalla del dispositivo, establezca un número de dp (píxeles independientes de la densidad). Por ejemplo, 16dp significa 16 píxeles independientes de la densidad.

Sugerencia: si cambia el atributo **layout_width** usando un menú emergente, el atributo **layout_width** se establece en cero porque no hay una dimensión establecida. Esta configuración es la misma que match_constraint: el elemento UI puede expandirse tanto como sea posible para cumplir con las restricciones y la configuración de márgenes.

El panel **Atributos** ofrece acceso a todos los atributos que puede asignar a un elemento de Vista. Puede ingresar valores para cada atributo, como los atributos de android: id, background, textColor y text.

#### <a id="editando"></a> Editando el archivo XML directamente

A veces es más rápido y más fácil editar el código XML directamente, especialmente al copiar y pegar el código para obtener vistas similares.

Para ver y editar el código XML, abra el archivo de diseño XML. El editor de diseño aparece con la pestaña Diseño en la parte inferior resaltada. Haga clic en la pestaña Texto para ver el código XML. A continuación se muestra el código XML para un **LinearLayout** con dos elementos de botón con un **TextView** en el medio:

    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:app="http://schemas.android.com/apk/res-auto"
      xmlns:tools="http://schemas.android.com/tools"
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:orientation="vertical"
      tools:context="com.example.android.hellotoast.MainActivity">

      <Button
        android:id="@+id/button_toast"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginEnd="8dp"
        android:layout_marginStart="8dp"
        android:layout_marginTop="8dp"
        android:background="@color/colorPrimary"
        android:onClick="showToast"
        android:text="@string/button_label_toast"
        android:textColor="@android:color/white" />

      <TextView
        android:id="@+id/show_count"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center_vertical"
        android:layout_marginBottom="8dp"
        android:layout_marginEnd="8dp"
        android:layout_marginStart="8dp"
        android:layout_marginTop="8dp"
        android:background="#FFFF00"
        android:text="@string/count_initial_value"
        android:textAlignment="center"
        android:textColor="@color/colorPrimary"
        android:textSize="160sp"
        android:textStyle="bold"
        android:layout_weight="1"/>

      <Button
        android:id="@+id/button_count"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="8dp"
        android:layout_marginEnd="8dp"
        android:layout_marginStart="8dp"
        android:background="@color/colorPrimary"
        android:onClick="countUp"
        android:text="@string/button_label_count"
        android:textColor="@android:color/white" />
    </LinearLayout>
    
##### Atributos XML (Vista de Propiedades)

Las vistas tienen propiedades que se definen dónde aparece una vista en la pantalla, su tamaño, cómo se relaciona la vista con otras vistas y cómo responde a la entrada del usuario. Al definir vistas en XML o en el panel Atributos del editor de diseño, las propiedades se conocen como **atributos**.

Por ejemplo, en la siguiente descripción XML de un *TextView*, **android:id*, android:layout_width, android:layout_height, android:background** son atributos XML que se traducen automáticamente en las propiedades de TextView:

    <TextView
       android:id="@+id/show_count"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:background="@color/myBackgroundColor"
       android:textStyle="bold"
       android:text="@string/count_initial_value" />

##### Identificando una vista

Para identificar de forma única una Vista y hacer referencia a ella desde su código, debe asignarle un ID. El atributo android: id le permite especificar una identificación única, un identificador de recursos para una Vista. Con el "+" se especifica que se está añadiendo un nuevo identificador.

Por ejemplo:
> android:id="@+id/button_count"


##### Haciendo referencia a una vista

Para hacer referencia a un identificador de recurso existente, omita el símbolo más (+). Por ejemplo, para referirse a una Vista por su id en otro atributo, como android: layout_toLeftOf (descrito en la siguiente sección) para controlar la posición de una Vista, debe usar:
> android:layout_toLeftOf="@id/show_count"

##### Posicionando una vista

Algunos atributos de posicionamiento relacionados con el diseño son necesarios para una Vista o un *ViewGroup*, y aparecen automáticamente cuando agrega la Vista o el Grupo de vistas al diseño XML.

######  Posicionamiento con LinearLayout

Se requiere que LinearLayout tenga estos atributos establecidos:

  * android:layout_width
  * android:layout_height
  * android:orientación

Los atributos *android:layout_width* y *android:layout_height* pueden tomar uno de tres valores:

  * **match_parent** expande el elemento UI para llenar su padre por ancho o alto. Cuando LinearLayout es el ViewGroup raíz, se expande al tamaño de la pantalla del dispositivo. Para un elemento de la interfaz de usuario dentro de un grupo de vista raíz, se expande al tamaño del grupo de vista principal.
  * **wrap_content** reduce el elemento UI al tamaño de su contenido. Si no hay contenido, el elemento se vuelve invisible.
  * **Utilizar un número fijo de dp (píxeles independientes de la densidad)** para especificar un tamaño fijo, ajustado para el tamaño de la pantalla del dispositivo. Por ejemplo, 16dp significa 16 píxeles independientes de la densidad. Los píxeles independientes de la densidad y otras dimensiones se describen en "Dimensiones" en este capítulo.

La propiedad android:orientatión puede ser:
  * **horizontal**: las vistas están ordenadas de izquierda a derecha.
  * **vertical**: las vistas se organizan de arriba a abajo.

Otros atributos relacionados con el diseño incluyen:

  * **android:layout_gravity**: este atributo se usa con un elemento de la interfaz de usuario para controlar dónde está dispuesto el elemento dentro de su elemento primario. Por ejemplo, el siguiente atributo centra el elemento UI horizontalmente en el ViewGroup principal:

> android: layout_gravity="center_horizontal"

  * El **padding** es el espacio, medido en píxeles independientes de la densidad, entre los bordes del elemento UI y el contenido del elemento, como se muestra en la siguiente figura.
  
  ![Propiedad de padding](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/1-2-c-layouts-and-resources-for-the-ui/dg_padding_annotated.png)
  
En la figura anterior: (1) El *Padding* es el espacio entre los bordes de TextView (líneas discontinuas) y el contenido de TextView (línea continua). El relleno no es lo mismo que el margen, que es el espacio desde el borde de la Vista hasta su padre.

El tamaño de una vista incluye su relleno. Los siguientes son atributos de *padding* comúnmente utilizados:
  * **android:padding**: establece el padding de los cuatro bordes.
  * **android:paddingTop**: establece el padding del borde superior.
  * **android:paddingBottom**: establece el padding del borde inferior.
  * **android:paddingLeft**: establece el padding del borde izquierdo.
  * **android:paddingRight**: establece el padding del borde derecho.
  * **android:paddingStart**: establece el padding del inicio de la vista, en píxeles. Se usa en lugar de los atributos de relleno enumerados anteriormente, especialmente con vistas largas y estrechas.
  * **android:paddingEnd**: establece el padding del borde final de la vista, en píxeles. Se utiliza junto con Android: paddingStart.

*Sugerencia*: para ver todos los atributos XML de un LinearLayout, consulte la sección Resumen de la definición de la clase LinearLayout. Otros diseños de layout, como RelativeLayout y AbsoluteLayout, también enumeran sus atributos XML en las secciones de Resumen.  

######  Posicionamiento con RelativeLayout

Otro grupo de vistas útil para el diseño es RelativeLayout, que se puede utilizar para colocar elementos de vista secundarios relacionados entre sí o con el padre. Los atributos que puede usar con RelativeLayout incluyen lo siguiente:

  * **android:layout_toLeftOf**: coloca el borde derecho de esta vista a la izquierda de otra vista (identificada por su ID).
  * **android:layout_toRightOf**: coloca el borde izquierdo de esta vista a la derecha de otra vista (identificada por su ID).
  * **android:layout_centerHorizontal**: Centra esta vista horizontalmente dentro de su padre.
  * **android:layout_centerVertical**: centra esta vista verticalmente dentro de su padre.
  * **android:layout_alignParentTop**: coloca el borde superior de esta vista para que coincida con el borde superior del padre.
  * **android:layout_alignParentBottom**: coloca el borde inferior de esta vista para que coincida con el borde inferior del padre.

Para obtener una lista completa de los atributos de los elementos de la subclase *View* y ver en un RelativeLayout, consulte [RelativeLayout.LayoutParams](https://developer.android.com/reference/android/widget/RelativeLayout.LayoutParams.html).

##### Atributos relacionados con el estilo

Asimismo, se pueden especificar los atributos de estilo para personalizar la apariencia de una vista. Una *View* que no tiene atributos de estilo, como *android:textColor*, *android:textSize* y *android:background* si no que adopta los estilos definidos en el tema de la aplicación.

Los siguientes son atributos relacionados con el estilo utilizados en la lección sobre el uso del editor de diseño:

  * android:background: especifica un color o recurso dibujable para usar como fondo.
  * android:text: especifica el texto que se mostrará en la vista.
  * android:textColor: especifica el color del texto.
  * android:textSize: especifica el tamaño del texto.
  * android:textStyle:especifica el estilo del texto, como negrita.

#### <a id="archivos"></a> Archivos de recursos

Los archivos de recursos son una forma de separar los valores estáticos del código para que no tenga que cambiar el código en sí para cambiar los valores. Puede almacenar todas las cadenas, diseños, dimensiones, colores, estilos y texto de menú por separado en archivos de recursos.

Los archivos de recursos se almacenan en carpetas ubicadas en la carpeta **res** en el panel *Project>Android*. Estas carpetas incluyen:

  * **Drawable**: para imagenes e iconos.
  * **Layout**: para archivos de diseño de las diferentes activites
  * **Menu**: para elementos de menú
  * **Mipmap**: para colecciones precargadas y optimizadas de íconos de aplicaciones utilizados por el Lanzador
  * **Values**: para colores, dimensiones, cadenas y estilos (atributos de tema)

La sintaxis para hacer referencia a un recurso en un diseño XML es la siguiente:

> @nombre_paquete:tipo_recurso/nombre_recurso

  * El nombre del paquete es el nombre del elemento en el que se encuentra el recurso. El nombre del paquete no es necesario cuando hace referencia a los recursos que están almacenados en la carpeta res de su proyecto, porque estos recursos son del mismo paquete.
  * El tipo de recurso es la subclase R para el tipo de recurso. Consulte [Tipos de recursos](https://developer.android.com/guide/topics/resources/available-resources.html) para obtener más información sobre los tipos de recursos y cómo hacer referencia a ellos.
  * El nombre del recurso es el nombre de archivo del recurso sin la extensión, o el valor del atributo *android:name* en el elemento XML.

Por ejemplo, la siguiente declaración de diseño XML establece el atributo *android:text* en un recurso de cadena:
> android:text="@string/button_label_toast"


  * Ningún nombre de paquete se inserta porque el recurso está dentro del fichero *strings.xml* del proyecto
  * El tipo de recurso es un tipo *string*
  * El nombre del recurso es *button_label_toast*.
  
 Otro ejemplo: esta declaración de diseño XML establece el atributo *android:background* en un recurso de color, y como el recurso está definido en el proyecto (en el archivo colors.xml), el nombre de paquete no se especifica:

> android:background="@ color/colorPrimary"

En el siguiente ejemplo, la declaración de diseño XML establece el atributo android:textColor en un recurso de color. Sin embargo, el recurso no está definido en el proyecto, pero es suministrado por Android, por lo que debe especificar el nombre de paquete, que es android, seguido de dos puntos:

> android:textColor="@android:color/white"

Sugerencia: para obtener más información sobre cómo acceder a los recursos desde el código, consulte [Cómo acceder a los recursos](http://developer.android.com/guide/topics/resources/accessing-resources.html). Para las constantes de color de Android, consulte los [recursos de R.color estándar de Android](http://developer.android.com/reference/android/R.color.html).

###### Ficheros de recursos de valores

Mantener valores como cadenas y colores en archivos de recursos separados facilita su gestión, especialmente si los usa más de una vez en sus layouts.

Por ejemplo, es esencial mantener las cadenas en un archivo de recursos separado para traducir y localizar su aplicación, de modo que pueda crear un archivo de recursos de cadena para cada idioma sin cambiar su código. Los archivos de recursos para imágenes, colores, dimensiones y otros atributos son útiles para desarrollar una aplicación para diferentes tamaños de pantalla y orientaciones de dispositivos.

###### Cadenas

Los recursos de cadena se encuentran en el archivo strings.xml (dentro de **res>values** en el panel **Project> Android**). Puede editar este archivo directamente abriéndolo en el panel del editor:

    <resources>
     <string name="app_name">Hello Toast</string>
     <string name="button_label_count">Count</string>
     <string name="button_label_toast">Toast</string>
     <string name="count_initial_value">0</string>
    </resources>
    
El nombre (por ejemplo, button_label_count) es el nombre del recurso que se usa en el código XML, tal y como se muestra en el siguiente atributo:

> android:text="@string/button_label_count"

#### <a id="respondiendo"></a> Respondiendo a los gestos
#### <a id="practicas"></a> Prácticas relacionadas
#### <a id="aprende"></a> Aprende más
