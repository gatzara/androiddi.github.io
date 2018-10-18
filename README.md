# androiddi.github.io
Apartat d'Android en el mòdul de DI de DAM

## Construyendo la primera app
##Title

###Place 1

Hello, this is some text to fill in this, [here](#place-2), is a link to the second place.

###Place 2

Place one has the fun times of linking here, but I can also link back [here](#place-1).

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

#### <a href=”#puntos”></a> Puntos de vista

La interfaz de usuario consta de una jerarquía de objetos llamados vistas: cada elemento de la pantalla es una vista. La clase Vista representa el bloque de construcción básico para todos los componentes de la interfaz de usuario y la clase base para las clases que proporcionan componentes de la interfaz de usuario interactivos, como botones, casillas de verificación y campos de entrada de texto.

Una vista tiene una ubicación, expresada como un par de coordenadas izquierda y superior, y dos dimensiones, expresadas como un ancho y una altura. La unidad de ubicación y dimensiones es el píxel independiente de densidad (dp).

El sistema Android proporciona cientos de subclases de vista predefinidas. Las subclases de vista de uso común descritas en varias lecciones incluyen:

    TextView para mostrar texto
    EditText para permitir al usuario ingresar y editar texto
    Botón y otros elementos seleccionables (como RadioButton, CheckBox y Spinner) para proporcionar un comportamiento interactivo
    ScrollView y RecyclerView para mostrar elementos desplazables
    ImageView para mostrar imágenes
    ConstraintLayout y LinearLayout para contener otras vistas y colocarlas

Puede definir una vista para que aparezca en la pantalla y responder a un toque de usuario. También se puede definir una vista para aceptar el ingreso de texto o para que sea invisible hasta que sea necesario.

Puede especificar Ver elementos en archivos de recursos de diseño. Los recursos de diseño se escriben en XML y se enumeran dentro de la carpeta de diseño en la carpeta res en el panel Proyecto> Android.


#### <a href=”#editor”></a> Editor de diseño
