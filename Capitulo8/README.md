# Background Images

CSS3 introduce una serie de propiedades nuevas y ampliadas que están destinadas a decorar elementos de forma mucho más sencilla, y los creadores de
navegadores se han apresurado a implementarlas y agregar también varias de sus propias implementaciones. 
Debido a la gran demanda de los desarrolladores web, los navegadores ya implementan bien las nuevas propiedades que ofrece.Internet Explorer 9 
implementó completamente las propiedades y los cambios enumerados en este capítulo.
Las imágenes de fondo han sido parte de CSS durante muchos años, pero a diferencia de las versiones anteriores, en CSS3, es posible aplicar varias 
imágenes a los elementos y cambiar el tamaño de esas imágenes sobre la marcha. 

## Actualizaciones de las propiedades de fondo existentes

### Posición de fondo

La propiedad posición de fondo en CSS2.1 acepta dos valores: una palabra clave para cada lado del cuadro (parte superior derecha,y así sucesivamente),
o valores de longitud o porcentaje que establecen una posición relativa a la esquina superior izquierda del elemento al que se aplica. Esto está bien 
para muchas tareas, pero en realidad no proporciona el control preciso que deseamos al diseñar las páginas.
En CSS3, la propiedad ahora acepta hasta cuatro valores: puede usar palabras clave para especificar un lado y luego valores de longitud o porcentaje
para la distancia relativa desde ese lado. Observe el siguiente ejemplo:

     .foo { background-position: right 10em bottom 50%; }

La imagen de fondo del elemento "foo" se colocará a 10 em desde la derecha y al 50 % desde abajo. Este posicionamiento habría sido muy difícil en 
CSS2.1; había que conocer los anchos de todos los elementos involucrados y que no cambiaran.

###  Archivo adjunto de fondo

La forma en que se desplaza una imagen de fondo en la ventana gráfica está determinada por el archivo adjunto de fondo propiedad. Los valores 
permitidos en CSS2.1 son: Desplazarse (el valor predeterminado), lo que significa que la imagen no se desplaza con el elemento al que se aplica, pero sí con la ventana gráfica,
y fijado,lo que significa que la imagen no se desplaza ni con su elemento ni con la ventana gráfica.

Un nuevo valor de local se introduce en CSS3; este valor permite que una imagen se desplace tanto con su elemento como con la ventana gráfica. 
El nuevo valor es compatible con IE9+ y todos los demás navegadores de escritorio modernos importantes. Los navegadores móviles, sin embargo, tienden 
a utilizar diferentes mecanismos de diseño de ventanas gráficas en los que los elementos fijos realmente no funcionan, por lo que probablemente 
obtendrás un comportamiento inesperado (o no) en ellos.

### Repetición de fondo

En CSS2.1, la propiedad repetición de fondo acepta uno de cuatro valores posibles:no- repetir, repetir, repetir-x,yrepetir-y.
Con estos valores, puede colocar imágenes en mosaico horizontal o verticalmente (o ambas) a lo largo de un elemento, pero no permiten ningún control
más preciso que ese. CSS3, sin embargo, amplía la utilidad de la propiedad de dos maneras: un par de propiedades nuevas y un ajuste en la sintaxis.

La primera de las nuevas propiedades es espacio,que configura la imagen de fondo para que se repita en el elemento que la contiene tantas veces como 
sea posible sin recortar la imagen. Todas las repeticiones (excepto la primera y la última) están espaciadas igualmente, por lo que la imagen se 
distribuye uniformemente.
El segundo es redondo,lo que también configura la imagen de fondo para que se repita tantas veces como sea posible sin recortar, pero en lugar de 
espaciar las repeticiones por igual, las imágenes se escalan de modo que un número entero de imágenes llene el elemento contenedor.

Resultados del "Ejemplo 1", del documento Ejemplos_Capitulo8.css subido en el presente repositorio;
El elemento de la izquierda es de referencia; tiene el valor predeterminado repetición de fondo valor de repetir y muestra el comportamiento que se
esperaría actualmente. El elemento del medio tiene un valor de espacio, y el número máximo de imágenes que se pueden colocar en mosaico sin recortar
ni escalar se muestran con espacios vacíos entre ellas. Finalmente, el elemento de la derecha tiene un valor deredondo,que calcula el número entero
máximo que puede caber en el elemento contenedor tanto horizontal como verticalmente, escalando la imagen según sea necesario.

![Imagen 1 ilustrando el capitulo 8](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo8/Imagenes/C8/Imagen1_C8.png)

También mencioné un cambio en la sintaxis. Puede controlar el mosaico en los dos ejes diferentes de forma independiente, ya que la propiedad ahora 
acepta dos valores. El primer valor controla el mosaico en el eje horizontal, el segundo en el vertical. Entonces, si desea que una imagen de fondo
se repita con redondeo en vertical y espaciado en horizontal, se usa el siguiente código:

     .foo { background-repeat: round space; }

![Imagen 2 ilustrando el capitulo 8](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo8/Imagenes/C8/Imagen2_C8.png)

## Multiple Background images

La primera característica nueva en el módulo Fondos y bordes no es una propiedad nueva, sino una extensión de una existente o, mejor dicho, de varias
existentes. Usando CSS2.1, solo puedes aplicar una única imagen de fondo a un elemento, pero en CSS3, (casi todas) las propiedades background-* ahora 
aceptan múltiples valores, por lo que puede agregar muchas imágenes de fondo a un elemento.

Para hacer esto, solo necesita enumerar los valores separados por comas. Por ejemplo:

     E { background-image: value, value; }

Resultados del "Ejemplo 2", del documento Ejemplos_Capitulo8.css subido en el presente repositorio; Las capas se crean en orden inverso; es decir, 
la primera capa de la lista se convierte en la capa superior, y así sucesivamente. En el código de ejemplo,mono.svg es una capa arriba paisaje.jpg.
La propiedad posición de fondo sigue el mismo orden: el paisaje se sitúa en 50% izquierda y 50% superior (el centro horizontal y vertical) de su 
elemento contenedor y el mono en 95% izquierda y 85% arriba.

![Imagen 3 ilustrando el capitulo 8](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo8/Imagenes/C8/Imagen3_C8.png)

Si una propiedad tiene menos valores que capas de fondo, los valores se repetirán. En este ejemplo eso significano repetirse aplicará a todas las
capas de fondo.
Puede utilizar varios valores con el fondo propiedad taquigráfica; Al igual que con las propiedades individuales, sólo necesita proporcionar una 
lista separada por comas. 

Casi todas las propiedades de fondo pueden tener múltiples valores sin embargo .color de fondo, es la excepción, ya que la capa de color siempre se
apilará debajo de todas las demás capas de fondo. Si desea especificar un color de fondo al utilizar la propiedad abreviada, debe colocarlo en la 
última instancia de la lista separada por comas. En el caso del siguiente código de ejemplo, estaría en la instancia con la imagen del paisaje:

     h2 {
          background:
          url('monkey.svg') no-repeat 95% 85%,
          url('landscape.jpg') no-repeat 50% 50% #000;
        }

## Imágenes de fondo escaladas dinámicamente

Una nueva propiedad de CSS3 es tamaño de fondo. Esta propiedad, como probablemente puedas adivinar, te permite establecer el tamaño de las imágenes
de fondo. Aquí está la sintaxis:

     E { background-size: value; }

El valor de esta propiedad puede ser un par de longitudes o porcentajes, una única longitud o porcentaje o una palabra clave. Si se utiliza un par,
la sintaxis es la siguiente:

     E { background-size: width height; }

Para cambiar el tamaño de una imagen de fondo para que tenga 100 px de ancho y 200 px de alto, utilice:

     div { background-size: 100px 200px; }

La longitud puede ser cualquier unidad de medida estándar. Si utiliza porcentajes, la dimensión se basa en el elemento contenedor,no la imagen de 
fondo. Entonces un ancho y alto de 100%,por ejemplo, estirará la imagen de fondo para llenar el contenedor. Para que la imagen aparezca en su tamaño
natural, utilice el auto palabra clave.
Si solo especifica un valor único, ese valor se considera el ancho y luego a la altura se le asigna el valor predeterminado de auto.Por tanto, 
estos dos ejemplos son exactamente equivalentes:

     div { background-size: 100px auto; }
     div { background-size: 100px; }

Resultados del "Ejemplo 3", del documento Ejemplos_Capitulo8.css subido en el presente repositorio; Un mono tiene una vertical. tamaño de fondo
del 80%, el siguiente 15%, y el último, el 50%; En todos los casos, el tamaño horizontal se ha establecido en auto para mantener la imagen en 
proporción.

![Imagen 4 ilustrando el capitulo 8](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo8/Imagenes/C8/Imagen4_C8.png)

Además de los valores de longitud, hay dos palabras clave disponibles:contenery cubrir. El contener la palabra clave establece la imagen a escala 
(proporcionalmente) lo más grande posible, sin exceder ni la altura ni el ancho del elemento que la contiene;cubrir establece la imagen para 
escalar al tamaño de la altura o el ancho del elemento que la contiene, el que sea mayor.

Resultados del "Ejemplo 3.1", del documento Ejemplos_Capitulo8.css subido en el presente repositorio; El cuadro de la izquierda tiene el contener valor
de la palabra clave, de modo que la imagen de fondo llene el cuadro verticalmente (la longitud más corta); el cuadro de la derecha tiene el cubrir
valor de palabra clave, por lo que la imagen de fondo llena el cuadro horizontalmente (la longitud más larga) y se recorta en la parte superior e
inferior.

![Imagen 5 ilustrando el capitulo 8](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo8/Imagenes/C8/Imagen5_C8.png)

## Clip de fondo y origen

En CSS2, la posición de una imagen de fondo se define en relación con el límite exterior del relleno del elemento que la contiene, y cualquier 
desbordamiento se extiende por debajo de su borde. CSS3 introduce dos nuevas propiedades que brindan un control más granular sobre esta ubicación.
La primera propiedad es clip de fondo, que establece la sección del modelo de caja que se convierte en el límite donde se muestra el fondo (ya sea 
color o imagen). Aquí está la sintaxis:

     E { background-clip: box; }

El valor puede ser una de tres palabras clave:cuadro de borde, cuadro de contenido, caja de relleno o caja de borde. El valor predeterminado muestra
el fondo detrás del borde (puede verlo si usa un color de borde transparente o semiopaco). Un valor de caja de relleno muestra el fondo sólo hasta
el borde y no detrás del cuadro de contenido significa que el fondo se detiene en el relleno del elemento.

Resultados del "Ejemplo 3.1", del documento Ejemplos_Capitulo8.css subido en el presente repositorio; Se ha usado un borde semiopaco para que puedas ver
la pintura de la imagen debajo en el cuadro de la izquierda, que tiene el cuadro de borde valor. La caja central tiene la caja de relleno valor, y
como puede ver, el fondo se detiene en el límite del relleno. En el cuadro de la derecha, el valor es cuadro de contenido,para que el fondo no se 
vea detrás del relleno.

![Imagen 6 ilustrando el capitulo 8](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo8/Imagenes/C8/Imagen6_C8.png)

La segunda propiedad que le brinda un control más granular es origen de fondo. Usando origen de fondo,puede establecer el punto donde se calcula el
fondo para comenzar. Como mencioné antes, las posiciones de fondo de CSS2 se calculan en relación con el límite del relleno, pero origen-fondote 
permite cambiar eso. Aquí está la sintaxis:

     E { background-origin: box; }

El caja value acepta las mismas palabras clave que acaba de ver en clip de fondo: cuadro de borde, cuadro de contenido,y caja de relleno.

Resultados del "Ejemplo 3.1", del documento Ejemplos_Capitulo8.css subido en el presente repositorio; El mono está en una posición diferente en cada cuadro porque el posición de fondo se calcula en relación con un punto diferente en cada cuadro 
(agregué una cuadrícula de fondo para que sea un poco más fácil de ver).
El posición de fondo siempre se establece en 0 100%,que es la parte inferior izquierda. El punto desde el que se mide la parte inferior izquierda 
cambia dependiendo de la origen-fondo valor, sin embargo. En el primer cuadro, el fondo se origina en el límite del borde; en el segundo, desde el
límite del acolchado; y en el tercero, desde el límite del cuadro de contenido.

![Imagen 7 ilustrando el capitulo 8](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo8/Imagenes/C8/Imagen7_C8.png)

Un par de cosas a tener en cuenta: Primero, esta propiedad no tiene ningún efecto Si el posición de fondose establece en fijado.En segundo lugar, 
ambos clip de fondoy origen-fondo acepte múltiples valores.

## Acceso directo de fondo actualizado

La propiedad fondo de acceso directo se ha actualizado para incluir valores para el tamaño de fondo, clip de fondo,y origen-fondo propiedades. 
Valores para tamaño de fondo debe seguir inmediatamente aquellos para posición de fondo y estar separados por una barra diagonal, así:

     E { background: url('bar.png') no-repeat 50% 50% / 50% auto; }

En este caso, la imagen de fondo,barra.png, se colocará en el punto muerto del elemento, con un ancho establecido en el 50% del elemento y una 
altura automática.

Paraclip de fondo y origen de fondo,si solo hay un valor de cuadro (caja de borde, caja de relleno o cuadro de contenido)está presente, ambas 
propiedades se establecerán en ese valor. Si se proporcionan dos valores de cuadro, el primero se establecerá en origen-fondoy el segundo en clip
de fondo.Como una ilustracion,tome este código abreviado:

     E { background: url('bar.png') no-repeat padding-box content-box; }

En este caso, el origen de la imagen de fondo será el cuadro de relleno y la imagen se recortará al cuadro de contenido.




















