# androiddi.github.io
Apartat d'Android en el mòdul de DI de DAM

## Construyendo la primera app

### Layouts y recursos para la interfaz de usuario

Contenido:
* [Puntos de vista](#puntos)
* [El editor de diseño](#editor)
* Editando XML directamente
* Archivos de recursos
* Respondiendo a ver clics
* Practicas relacionadas
* Aprende más

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

#### <a id="editor"></a> Editor de diseño
