# MEDIAS QUERIES

![Media Queries](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo2/Imagenes/media-queries-blog.jpeg)

CSS dispone desde hace tiempo de una forma de servir diferentes estilos a diferentes tipos de medios, utilizando el atributo media del elemento link:

    <link href="style.css" rel="stylesheet" media="screen">

Pero este enfoque tiene una serie de defectos, entre ellos que utilizarlo es como blandir un instrumento bastante contundente cuando la pantalla en cuestión
puede tener un tamaño de entre 3,5 y 32 pulgadas. La lista de tipos es demasiado amplia y muchos no son compatibles con los dispositivos a los que se dirigen 
el tipo tv. En vista de ello, no es sorprendente que el W3C haya empezado a desaprobar el uso de tipos de medios.
Estas consultas amplían los tipos de medios proporcionando una sintaxis de consulta que permite servir estilos mucho más específicos al dispositivo del usuario, 
ofreciéndole una experiencia personalizada. 

Las consultas de medios te dan la libertad de crear sitios web que son realmente independientes del dispositivo, ofreciendo a tus usuarios la mejor experiencia
posible independientemente de cómo decidan visitar tu sitio.
El módulo Media Queries tiene estatus de Recomendación del W3C, por lo que se considera un estándar. 

## Ventajas de las consultas multimedia

Las consultas de medios detectan los dispositivos en función de sus atributos, por lo que no se necesitan scripts de rastreo del navegador. Permiten orientar 
las hojas de estilo directamente a las capacidades de un dispositivo, de modo que si se detecta un dispositivo con una pantalla pequeña, las reglas CSS se 
adaptarán a ese tamaño de pantalla, eliminando elementos superfluos, sirviendo imágenes más pequeñas y haciendo el texto más claro 

## Sintaxis

Una consulta de medios establece un parámetro (o una serie de parámetros) que activa las reglas de estilo asociadas si el dispositivo utilizado para ver la página
tiene propiedades que coinciden con ese parámetro. Las consultas de medios se pueden utilizar de tres maneras, que coinciden con las distintas formas en que se 
puede aplicar CSS a un documento. 

La primera es llamar a una hoja de estilo externa utilizando el elemento link:

     <link href="file" rel="stylesheet" media="media lógica y (expresión)>

La segunda es llamar a una hoja de estilo externa utilizando la directiva @import:

     @import url('archivo') medios lógicos y (expresión);

La tercera es utilizar consultas de medios en un elemento de estilo incrustado o en la propia hoja de estilo con la regla @media extendida:

     @media logic media and (expression) { rules }


Los valores de tipo de medio más comunes son pantalla e impresión, y al igual que con la sintaxis actual, puede utilizar una lista separada por comas para elegir
múltiples consultas de medios.

Si se omite, el tipo de medio por defecto es **all**, por lo que s i está escribiendo reglas que se aplicarán a todos los tipos de medios no necesitará
especificarlas en el constructor de la consulta de medios; siendo  ese el caso, estos ejemplos son funcionalmente idénticos:

     @media all and (expresión) { reglas } 
     @media (expresión) { reglas }


El primer atributo nuevo de la regla @media es logic. Esta palabra clave opcional puede tener el valor de **only** o **not**:

     @media only media and (expresión) { reglas } 
     @media not media and (expresión) { reglas }

El valor **only** es útil principalmente si desea ocultar la regla a navegadores antiguos que no soportan la sintaxis; para los navegadores que sí la soportan, **only** 
se ignora efectivamente. El valor **not** se utiliza para negar la consulta; se utiliza **not** para aplicar los estilos si no se cumplen los parámetros establecidos.
Si utiliza lógica o medios en su consulta, también deberá utilizar el operador y, como en los ejemplos anteriores, para combinarlos con el atributo de expresión 
requerido. Este atributo se utiliza para establecer parámetros que ofrecen funcionalidad más allá del tipo de medio. Estos parámetros se conocen como 
características de medios y son fundamentales para la potencia de las consultas de medios

## Medios de comunicación
Las características multimedia son información sobre el dispositivo que se está utilizando para mostrar la página web: sus dimensiones, resolución, etc. Esta 
información se utiliza para evaluar una expresión, cuyo resultado determina qué reglas de estilo se aplican. Esa expresión podría ser, por ejemplo, "aplicar 
estos estilos sólo en dispositivos que tengan una pantalla de más de 480 píxeles" o "sólo en dispositivos orientados horizontalmente".
En las consultas de medios, la mayoría de las expresiones de características de medios requieren que se proporcione un valor:

     @media (feature: value) { rules }

Este valor es necesario para construir las expresiones de ejemplo que acabo de mencionar. En algunos casos, sin embargo, se puede omitir el valor y simplemente 
comprobar la existencia de la característica de los medios de comunicación en sí contra la expresión:

     @media (feature) { rules }

## Anchura y altura

La función de anchura del medio describe la anchura de la ventana gráfica de representación del tipo de medio especificado, lo que, en la práctica, suele 
significar la anchura actual del navegador (incluida la barra de desplazamiento) para los sistemas operativos de escritorio. La sintaxis básica requiere un valor 
de longitud:

     @media (width: 600px) { rules }

En este caso, las reglas se aplican sólo a los navegadores que están configurados para tener exactamente 600px de ancho, lo que probablemente es demasiado
específico. width también acepta uno de dos prefijos, max- y min-, lo que permite comprobar una anchura mínima o máxima:

     @media (max-width: 480px) { rules } 
     @media (min-width: 640px) { rules }

La primera consulta aplica las reglas en navegadores que no superan los 480px de ancho, y la segunda en navegadores que tienen al menos 640px de ancho.
Veamos un ejemplo práctico. En este caso, aprovecharé el tamaño de las ventanas de los navegadores con una cabecera decorativa para las ventanas más anchas
(se han omitido algunas reglas para mayor claridad):

     @media (min-width: 400px) {
      h1 { background: url('landscape.jpg'); }
    }
Esta consulta de medios comprueba si las ventanas del navegador tienen al menos 400px de ancho y aplica una imagen de fondo al elemento h1 cuando es así.

La función de medios de altura funciona de la misma manera, salvo que se dirige a los navegadores en función de su altura en lugar de su anchura. La sintaxis es 
la misma que la de anchura y también permite utilizar prefijos max- y min-:

     @media (altura: valor) { reglas }
     @media (max-height: value) { rules } @media (min-height: value) { rules }


Sin embargo, debido a la prevalencia del desplazamiento vertical, la altura se utiliza con mucha menos frecuencia que la anchura.

## Proporción de píxeles

En general, la unidad de píxel CSS (px) es una medida de un solo píxel en la pantalla del ordenador: si la ventana gráfica de tu navegador tiene 1024 píxeles de 
ancho y le das a un elemento una anchura de 1024px, esperas que ocupe toda la longitud horizontal de la ventana gráfica. Sin embargo, muchos dispositivos nuevos, 
sobre todo smartphones y tabletas, tienen pantallas de altísima resolución, lo que hace que un elemento de 1024 píxeles de ancho parezca muy pequeño y difícil de 
leer.
Para evitarlo, estos dispositivos más nuevos suelen tener un píxel CSS nocional, separado de los píxeles físicos del dispositivo, lo que permite acercar y alejar
el contenido y obtener una alta fidelidad gráfica en la pantalla pequeña. La relación entre píxeles físicos y píxeles CSS se conoce como relación de píxeles del
dispositivo (DPR). El iPhone 5S, por ejemplo, tiene un DPR de 2, lo que significa que un píxel CSS equivale a 4 píxeles físicos: 2 horizontales y 2 verticales.

Lo que eso significa en la práctica es que, aunque el iPhone 5S (por ejemplo) tiene una resolución física de 640×1136, tiene una resolución CSS de 320×568 
-exactamente la mitad de las dimensiones, ya que cada píxel CSS equivale a dos píxeles físicos, tanto horizontal como verticalmente
Aunque este alto DPR hace que el contenido escalable -como el texto y los gráficos vecinales- sea nítido y claro, las imágenes de mapa de bits pueden sufrir una
gran pérdida de calidad cuando se ven en pantallas de alta resolución. Para evitar este problema, existe una nueva función multimedia, llamada resolución, que
permite orientar los dispositivos en función de su DPR:

     @media media and (resolution: value) { rules }
 
El valor de la resolución es un número con una unidad de resolución: puntos por pulgada (DPI), puntos por centímetro (DPCM) o, lo que es más pertinente para 
nosotros, puntos por píxel (DPPX). La unidad DPPX se asigna al DPR del dispositivo, de modo que para aplicar una regla a dispositivos que tienen un valor DPR de 
1,5, se utiliza esto:

     @media (resolution: 1.5dppx) { rules }
 
Al igual que con las demás funciones multimedia, también puede detectar las relaciones de píxeles máxima y mínima:

     @media (max-resolution: number) { rules } 
     @media (min-resolution: number) { rules }

Esta flexibilidad facilita el servicio de imágenes de fondo de mayor resolución a navegadores con mayor densidad de píxeles, como puede verse en este código:

     ❶ E { background-image: url('image-lores.png'); }
     ❷ @media (min-resolution: 1.5dppx) { background-image: url('image-hires.png');
     ❸	background-size: 100% 100%;
     }
     
La primera regla (❶) significa que los navegadores de dispositivos con una relación de píxeles "estándar"  (o  de baja resolución)  utilizarán la imagen estándar 
(image-lores.png), mientras que los dispositivos con una DPR de al menos 1,5 utilizarán en su lugar la imagen de alta resolución (image-hires.png) (❷).
Observe el uso de la propiedad desconocida background-size aquí (❸); esta propiedad debe usarse con imágenes de alta resolución para asegurar que no se muestren
más grandes que el elemento al que se aplican 


Chrome, Firefox e Internet Explorer 10+ admiten la función de medios de resolución, aunque IE lamentablemente no ha implementado el valor DPPX; para adaptarse a
IE, debe utilizar DPI, multiplicando el DPR requerido por 96 (el valor DPI de una pantalla estándar). He aquí un ejemplo:

     @media (resolución: 1.5dppx), (resolución: 144dpi) { reglas }
 
Safari no admite resolución, sino que utiliza una función de medios propia llamada -webkit-device-pixel-ratio (junto con las variantes max- y min-), que toma 
como valor un único número sin unidades que es la RPD objetivo. Por lo tanto, para adaptarse a todos los navegadores modernos, utilice esta regla:

     @media (resolution: 1.5dppx), (resolution: 144dpi), (-webkit-device-pixel-ratio: 2) { rules }

## Dispositivo Anchura y d Altura

Las propiedades de anchura y altura están relacionadas con las dimensiones de la ventana gráfica del navegador, pero ésta no siempre es tan grande como la 
pantalla en la que se muestra. Si necesitas orientarte al tamaño físico de la pantalla en lugar del tamaño de la ventana gráfica, puedes utilizar las propiedades
device-width y device-height y sus variantes min- y max-. No las usarás muy a menudo, pero para explicar por qué, necesito hacer un inciso.
En la sección anterior, expliqué la diferencia entre píxeles CSS y píxeles físicos. 

La anchura media feature se mide en píxeles CSS,y la anchura del dispositivo, en píxeles físicos. Para que el contenido sea legible y tenga un "tamaño natural"
en una pantalla pequeña, ambas dimensiones deben coincidir. Para ello, añada la metaetiqueta viewport en el encabezado del documento, como se indica a 
continuación:

     <meta name="viewport" content="width=device-width">
 
Cuando la meta etiqueta viewport con estos valores está presente en el encabezado de una página, los navegadores móviles pasan al "modo móvil", en el que la 
ventana gráfica se ajusta a las dimensiones ideales para ese dispositivo. El resultado es que el contenido se muestra a un tamaño más adecuado para el dispositivo.


La ventana gráfica de un navegador en un dispositivo móvil tiende a ser tan grande como la propia pantalla, por lo que ambas son básicamente equivalentes; y en los
navegadores de escritorio, lo más probable es que quieras que tu contenido sea relativo a la anchura de la ventana gráfica y no a la de la pantalla. Por estas
razones, la función media **device-width** resulta menos útil que **width**, y probablemente no la utilices demasiado en la práctica.
La etiqueta meta viewport se está estandarizando en CSS como **@viewport**

## Orientación

Si le preocupan menos las dimensiones reales del dispositivo de visualización, pero desea optimizar sus páginas para una visualización horizontal 
(como un navegador web típico de escritorio/portátil) o vertical (como un teléfono móvil o un lector de libros electrónicos), la función multimedia que necesita
es la ***orientación.*** Esta es su sintaxis:

     @media (orientation: value) { rules }
 
Puede ser una de las dos opciones de la palabra clave: **horizontal o vertical.** El valor horizontal se aplica cuando la anchura del navegador es mayor que su altura,
y el valor vertical se aplica cuando ocurre lo contrario. Aunque la orientación puede aplicarse a navegadores de escritorio, te resultará más útil cuando se trate
de dispositivos portátiles que el usuario pueda girar fácilmente, como smartphones y tabletas.
Por ejemplo, puede utilizar la orientación para mostrar un menú de navegación horizontal o vertical, dependiendo de la orientación del navegador del visitante. 
El código es el siguiente:

     ul { overflow: hidden; } li { float: left; }
     @media (orientation: portrait) {
 
     li { float: none; }
     }
 
Por defecto, los elementos li tienen un valor de flotación izquierda, lo que hace que se apilen horizontalmente en la página. Si la misma página se visualiza con 
orientación vertical (ya sea redimensionando el navegador para que sea más alto que ancho o visualizando la página en un dispositivo con orientación vertical), se 
elimina la posición flotante y los elementos li se apilan verticalmente. 

Como sólo hay dos valores posibles para la función de orientación, si aplica reglas diferenciadoras utilizando un valor, el otro se convierte tácitamente en el 
opuesto. 


## Relación de aspecto

También puede crear consultas que se apliquen cuando se cumpla una determinada relación entre anchura y altura. Utilice aspect-ratio para comprobar la relación 
de aspecto del navegador o device-aspect-ratio para comprobar la relación de aspecto del dispositivo. Esta es la sintaxis para estas dos funciones:

     @media (aspect-ratio: horizontal/vertical) { rules }
     @media (device-aspect-ratio: horizontal/vertical) { rules }
     
Los valores horizontal y vertical son enteros positivos que representan la relación entre la anchura y la altura (respectivamente) de la pantalla del dispositivo 
de visualización, de modo que una pantalla cuadrada sería 1/1 y una pantalla panorámica cinematográfica sería 16/9.

La selección por relación de aspecto está potencialmente plagada de advertencias. Por ejemplo, algunos fabricantes de dispositivos definen la pantalla panorámica
como 16/9, otros como 16/10 y otros como 15/10. Y un dispositivo puede no tener la relación de aspecto exacta.

Puede ser preferible utilizar las variantes max- y min- de aspect-ratio y device- aspect-ratio para aplicar las reglas. Considere este código en el que las reglas
en la consulta se aplican a cualquier elemento que tenga una relación de aspecto superior a 16/9:

     @media (min-device-aspect-ratio: 16/9) {...}

## Múltiples funciones multimedia

Puede encadenar varias consultas sobre el mismo tipo de medio añadiendo expresiones con el operador y:

     @media lógica media and (expresión) and (expresión) { reglas }
 
Esta sintaxis comprueba que ambas expresiones coinciden antes de aplicar las reglas seleccionadas. Por ejemplo, para comprobar si la pantalla es estrecha en un 
dispositivo con una relación de aspecto no superior a 15/10, se utiliza esta consulta:

     @media (max-device-aspect-ratio: 15/10) and (max-width: 800px) {...}
 
También puede utilizar una expresión "o" condicional añadiendo consultas adicionales en una lista separada por comas:

     @media lógica media y (expresión), lógica media y (expresión) { reglas }
 
Esto aplica reglas cuando cualquiera de los casos indicados es verdadero; en el siguiente ejemplo, las reglas se aplican a una pantalla en orientación horizontal 
o a un documento impreso en orientación vertical:

     @media screen and (orientation: landscape), print and (orientation: portrait) {...}
 
Por supuesto, también puede crear cualquier combinación de estas sintaxis.

## Desarrollo web Mobile-First

Hoy en día, las mejores prácticas para crear sitios web se basan en un método conocido como desarrollo mobile-first, que consiste en empezar a desarrollar para
pantallas más pequeñas antes de añadir activos más grandes y más complejos para los usuarios que acceden al sitio desde dispositivos más grandes.
La razón por la que se adoptó este método es la forma en que algunos navegadores cargan los activos de la página, como las imágenes, que se incluyen en las hojas
de estilo.

Los problemas surgieron porque algunos de los primeros usuarios de las consultas de medios, por ejemplo, aplicaban grandes imágenes de fondo a los elementos y 
luego escribían reglas para ocultarlas de los dispositivos móviles:

     E { background-image: url('huge-image.jpg'); } @media (max-width: 600px) {
     E { display: none; }
    }
    
Pero esas imágenes de fondo, a pesar de estar ocultas, seguían siendo descargadas por el navegador y se mantenían en la caché aunque no se reprodujeran. 
Este método aumenta el tiempo de carga de la página y consume ancho de banda, nada bueno para los usuarios de dispositivos móviles sin conexiones inalámbricas.
La forma mobile-first de crear tus páginas consiste en hacer primero una hoja de estilo básica, que se aplica a todos los navegadores, incluidos los móviles, y 
luego ir añadiendo progresivamente activos y funciones para usuarios con pantallas más grandes, cargados mediante una media query con la función min-width:

     @media (min-width: 600px) {
     E { background-image: url('huge-image.jpg'); }
    }

Este cambio significa que la imagen de fondo en cuestión nunca se carga en dispositivos con pantallas más pequeñas. Este enfoque puede extrapolarse a la carga de
hojas de estilo completas:

     <link href="basic.css" rel="stylesheet">
     <link href="desktop.css" rel="stylesheet" media="(min-width: 600px)">
     
Cuando las hojas de estilo se separan de esta forma, algunos navegadores optimizan la forma en que se cargan; en Chrome, por ejemplo, como el archivo desktop.css
no se aplica a dispositivos con un ancho de pantalla inferior a 600px, su carga se retrasa hasta después de que se hayan descargado más activos de alta prioridad, una optimización bastante útil.
Este enfoque mobile-first funciona para la gran mayoría de los navegadores de los últimos años; los navegadores realmente antiguos obtendrán la hoja de estilo 
básica en su lugar, lo que probablemente sea mejor para ellos.








