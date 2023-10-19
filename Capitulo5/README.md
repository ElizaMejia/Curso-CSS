# Fuentes Web

Se da la bienvenida al regreso de estas características en CSS3. La principal de ellas es la capacidad de especificar fuentes que aún no existen en el sistema 
del usuario, utilizando @font-face método, IE4 fue el primer navegador que permitió fuentes web, pero lo hizo con un formato propietario que impedía que 
otros navegadores hicieran lo mismo. Posteriormente, Microsoft presentó su formato al W3C para su consideración como estándar, pero mientras tanto, Firefox, 
Safari y Chrome respaldaban un conjunto diferente de formatos, eventualmente siguieron versiones posteriores de Internet Explorer.  

El módulo de fuentes CSS Nivel 3 (http://www.w3.org/TR/css3-fonts/) tiene el estado de Recomendación candidata y la mayor parte de las especificaciones ya se 
han implementado en los navegadores modernos , por lo que puede considerar que estas funciones son seguras de usar.

## La regla @font-face

Para mostrar fuentes web en sus páginas, primero debe definirlas usando @font-face regla. Esta regla establece el nombre y el tipo de fuente y proporciona al 
navegador la ubicación del archivo a utilizar. Aquí está la sintaxis básica:

     @font-face {
        (1) font-family: FontName;
        (2) src: (3)local('fontname'), (4)url('/path/filename.otf') (5)format('opentype');
     }
Analizaré un poco esta sintaxis. Primero, le doy un nombre a la fuente con el Font-family propiedad (1). Debería estar familiarizado con esta propiedad, 
aunque tiene un propósito ligeramente diferente dentro de la regla que cuando se usa en el bloque de declaración para un selector normal; aquí, se usa para 
declarar el nombre de una fuente, no para hacer referencia a ella. Al igual que el Font family propiedad en  CSS2.1, puede utilizar varias palabras 
separadas por espacios siempre que las incluya entre comillas simples.

El siguiente es el src Propiedad (2), que le indica al navegador la ubicación del archivo de fuente. Esta propiedad acepta algunos valores diferentes: 
local (3) utiliza el nombre de la fuente de origen para comprobar si la fuente ya está instalada en la máquina del usuario; y URL (4) proporciona una ruta a 
la fuente si no está disponible localmente. También se ha incluido el opcional format (5) sugerencia, utilizada para especificar el tipo de fuente

Puedo proporcionar muchos valores diferentes para el src propiedad separando los valores con comas, como lo hice en el ejemplo de código. Esto utiliza el 
poder de la cascada para permitir diferentes valores de retroceso.

Para usar la fuente que acabo de definir, solo necesito llamar su nombre en la pila de fuentes, como lo haría normalmente:

     E { font-family: FontName; }
     
Para ilustrar un ejemplo del mundo real, aplicaré la fuente Chunk (disponible para descargar de forma gratuita desde 
http://www.theleagueofmoveabletype.com/fonts/4-chunk/) a una h1 elemento usando @font-face Aquí está el código que se usara:

     @font-face {
        (1)font-family: ChunkFive;
        src: (2)local('ChunkFive'), (3)url('ChunkFive.woff') (4)format('woff'); }
       
    (5)h1.webfont { font-family: ChunkFive, sans-serif; }
     
El primer paso es nombrar mi fuente; He elegido Chunk five (1) porque puedo recordarlo fácilmente, pero podría usar cualquier nombre. A continuación 
proporciono valores a la src propiedad: local (2) utiliza el verdadero nombre de la fuente, ChunkFive, para comprobar si está disponible en mi sistema. 
Después de eso, ingreso una ruta relativa al archivo de fuente que quiero usar (3) y, finalmente, asigno un argumento de woff
Hacia formato valor (4).

En la última línea (5), Incluyo mi fuente recién definida en la pila de fuentes usando el valor de nombre que definí dentro de @font-face regla y aplicarla a 
todos h1 elementos con un clase de fuente web. Para ver cómo se muestra, aquí hay una comparación rápida usando el siguiente marcado:


     <h1>Alas, poor Yorick!</h1>
     <h1 class="webfont">Alas, poor Yorick!</h1>
   
# AQUI VA IMAGEN 1
     
## Definiendo diferentes Faces

La sintaxis de @font-face que se ha visto hasta ahora en este capítulo es bastante sencilla, pero sólo define un tipo de fuente, es decir, una única
permutación de weight, pendiente, etc. Si desea utilizar una cara diferente, como para negritas o cursivas, debe definir cada tipo de fuente individualmente. 
Para hacer esto, reutiliza el mismo nombre y agrega descriptores adicionales al @font-face regla:

     @font-face {
        (1) font-family: 'Gentium Basic';
        src: url('(2)GenBasR.woff') format('woff'); }
        
     @font-face {
        (3) font-family: 'Gentium Basic'; 
        (4) font-style: italic;
        src: url('(5)GenBasI.woff') format('woff'); }
        
     h1 { font-family: 'Gentium Basic', sans-serif; }
     
Aquí puedes ver que la primera @font-face La regla define el nombre de la fuente como Gentium Básico (1) y proporciona la URL de la fuente normal (2). 
El segundo @font-face la regla usa el mismo nombre de fuente (3) pero agrega el Estilo de fuente propiedad con el itálico (4),y la URL apunta a la 
fuente en cursiva (5).El estilo de cursiva se aplica de forma automática y adecuada, sin que tengas que definirlo en el CSS, como en este ejemplo de
marcado:

     <h1>I knew him, Horatio</h1>
     <h1><em>I knew him, Horatio</em></h1>

# AQUI VA IMAGEN 2
Puede definir cualquier número de variaciones de una fuente con este método utilizando diferentes propiedades de fuente en @font-face regla: 
Font-weight para establecer varios weights ,font-variant para versalitas, etc.

## Caras de fuente verdaderas versus artificiales

Una cosa que debe tener en cuenta cuando utiliza fuentes web es que debe definir un enlace a un archivo apropiado para cada fuente diferente que desee
utilizar. Si no lo hace, los navegadores intentarán recrear la cara artificialmente, a menudo con resultados desagradables.
 
Por ejemplo, si va a utilizar un estilo de cursiva en su página, debe asegurarse de definir también un estilo de cursiva en @Perfil delantero.He aquí una 
ilustración de cómo no para definir un peso en cursiva:

     @font-face {
           font-family: 'Gentium Basic';
           src: url('GenBasR.woff') format('woff');
     }
     h1 {
            font-family: 'Gentium Basic', sans-serif;
            font-style: italic;
     }
# AQUI VA IMAGEN 3
Puedes ver que el @font-face la regla utiliza la cara normal de la fuente Gentium Basic, pero el elemento h1 tiene un estilo en cursiva declarado.
Como puede ver, los dos ejemplos son bastante diferentes. La primera es la fuente Gentium Basic seleccionada inclinada para simular un estilo de cursiva
(usando el primer ejemplo de código); las letas son más grandes, ligeramente distorsionados y espaciados de manera inconsistente. La segunda es la
fuente en cursiva verdadera (usando el método correcto), que utiliza caracteres diseñados específicamente para este propósito.
Lo mismo se aplica a todas las diferentes fuentes: negrita, cursiva, negrita cursiva, etc.

## Una sintaxis @font-face “a prueba de balas”

La regla el @font-face existe desde hace bastante tiempo y se implementó en Internet Explorer desde 1997. Esto significa que conlleva algunos problemas 
heredados desafortunados en versiones anteriores de IE. Además, algunos problemas históricos relacionados con los formatos de fuentes pueden causar 
problemas de compatibilidad en versiones anteriores de otros navegadores.
Debido a estos problemas, necesita una solución para garantizar que @font-face funciona correctamente en todos los navegadores. 
 
### Usar fuentes locales
El local() valor para el src La propiedad se utiliza para comprobar si un usuario ya tiene la fuente definida instalada en su sistema; si el usuario la 
tiene, se puede aplicar la copia local en lugar de descargar una nueva copia. Local() Es una buena idea, pero tiene algunos inconvenientes. El primer 
inconveniente, y no el menor, es que local() ¡No es compatible con ninguna versión de Internet Explorer inferior a 9!
Otro inconveniente es que, en algunos casos, La regla @font-face no funciona bien con el software de administración de fuentes, ya que muestra caracteres 
incorrectos o abre un cuadro de diálogo para solicitar permisos para usar una fuente. Por estas razones, dejar e llocal() El valor de salida es 
generalmente más seguro.

### Formatos de fuente

El siguiente problema se presenta en forma de formatos diferentes y competitivos. Cuando @font-face se implementó originalmente, solo admitía la propiedad 
de MicrosoftOpenType integrado (EOT )formato, y este sigue siendo el único formato de fuente compatible con IE8 y versiones inferiores. Para complicar aún
más esto, IE9 provoca el @font-face regla que se infringe cuando el navegador se pone en modo de compatibilidad; Este es un caso extremo y cada vez es 
menos relevante, pero vale la pena señalarlo, ya que podemos solucionarlo simplemente en nuestra sintaxis a prueba de balas.

### La sintaxis final "a prueba de balas"

Para que la fuente elegida se muestre igual en todos los navegadores y en todas las plataformas, debes usar código en este formato:

     @font-face {
          font-family: 'Gentium Basic';
          (1) src: url('GenBkBasR.eot');
          (2) src: url('GenBasR.eot?#iefix') format('embedded-opentype'), 
          (3) url('GenBkBasR.woff') format('woff'),
          (4) url('GenBkBasR.ttf') format('truetype');
     }
La primera fuente que se especificará es EOT (1) para Internet Explorer 8 y versiones anteriores. Esta fuente tiene una regla propia, ya que la siguiente 
regla contiene la opción opcional format() pista; Esta sugerencia no es familiar para el antiguo IE8, por lo que se ignorará toda la regla. Pero es 
necesario incluir nuevamente la fuente EOT (2) para solucionar el problema de compatibilidad con IE9. A continuación, se define el formato WOFF (3) para
la mayoría de navegadores, seguido del formato TTF (4)para navegadores más antiguos, incluido Android 4.3 y versiones anteriores (recuerde que los 
navegadores ignorarán los formatos que no comprenden y, por lo tanto, no pueden cargar).

Como el problema de compatibilidad con IE9 cada vez es menos importante, puede omitir la segunda línea (2) a su discreción.
Para que esto funcione, el requisito principal es que la fuente elegida esté disponible en tres formatos diferentes. Para hacer esto más fácil, 
recomiendo encarecidamente usar @font-face Generador de Font Squirrel (http://www. fontsquirrel.com/fontface/ generator/). Simplemente cargue el 
archivo de fuente que desea usar y @font-face Generator lo convierte a todos los formatos relevantes, además de generar el CSS que necesita usar en
sus páginas. Esta herramienta es invaluable. Font Squirrel también tiene una biblioteca de fuentes que están listas para usar con @font-face
incrustar, ahorrándole la tarea de convertir.


## Licencia de fuentes para uso web

Muchas fundiciones de fuentes prohíben expresamente incrustar sus fuentes web en sus páginas usando @font-face. Lo prohíben porque las fuentes OpenType o 
TrueType vinculadas son fáciles de localizar y descargar y luego pueden usarse ilegalmente en aplicaciones tanto en línea como fuera de línea. 
El tipo de archivo WOFF se creó en respuesta a esto; WOFF es un formato exclusivo de la web y puede contener información sobre licencias para ayudar a 
localizar a un infractor de derechos de autor. Muchas fundiciones ya se han comprometido a vender este formato y espero que muchas más lo sigan.

En general, la mejor política es verificar que la fuente que elija tenga una licencia que le permita explícitamente usarla para incrustación web; No asuma 
que debido a que una fuente se puede descargar gratis, su uso en línea es gratuito. Dicho esto, muchas fuentes gratuitas de buena calidad que permiten la 
incrustación están disponibles en línea; algunos recursos se proporcionan en el Apéndice B.
Si bien la situación de las licencias está cambiando, muchos proveedores de servicios de fuentes web han creado mecanismos para incrustar fuentes
legalmente en sus páginas. Al agregar JavaScript a sus páginas, el proveedor está autorizado a servir los archivos de fuentes desde su red, por lo que
puede llamar a las familias de fuentes en sus pilas. El método se conoce como Fuentes como servicio (FaaS).
 
La mayoría de los proveedores de FaaS son comerciales y permiten un conjunto limitado de fuentes de forma gratuita, pero cobran una tarifa mensual o anual
para la mayoría. Los dos jugadores más importantes en esta categoría son probablemente Fontdeck (http:// fontdeck.com/) y Typekit (https://typekit.com/).
Otros proveedores sólo ofrecen fuentes gratuitas: Google Fonts (http://www.google.com/fonts/) siendo un ejemplo notable de esto. Cada proveedor tiene su
propia forma de incluir las fuentes con licencia en su sitio, generalmente mediante la inclusión de un archivo CSS o JS externo, o ambos.

## Un ejemplo de fuentes web del mundo real

# AQUI VA IMAGEN 4
En el ejemplo de la derecha, mezclé tres familias de fuentes bastante distintivas; muchos diseñadores probablemente le dirán que mezclar no es una buena 
idea en un sitio de producción, pero funciona bien para ilustrar mi punto. Independientemente de lo que piense sobre mis opciones de fuente, espero que al
menos esté de acuerdo en que el texto se ve más dinámico y atractivo con esas opciones aplicadas.

## Más propiedades de fuente

El módulo de fuentes web CSS3 no se limita a reintroducir la @font-face regla; también revive otras dos propiedades de fuente que se propusieron por 
primera vez para CSS2. Estas propiedades son potencialmente muy útiles para brindarle un control granular sobre sus fuentes; digo potencialmente porque, 
hasta el momento, no están ampliamente implementados.

### font-size-adjust

El único inconveniente de utilizar pilas de fuentes en CSS es que las fuentes pueden variar mucho en tamaño; La fuente de su primera elección puede verse
muy bien en 16px, pero si esa fuente no está disponible, la siguiente fuente alternativa puede parecer más pequeña o tener diferentes proporciones y ser 
más difícil de leer en ese tamaño. Para combatir esto, La propiedad font-size-adjust le permite alterar dinámicamente el tamaño de fuente propiedad para
garantizar una apariencia regular sin importar qué fuente se utilice de la pila. La propiedad font-size-adjust toma un único valor decimal; aquí está la 
sintaxis:

     E { font-size-adjust: number; }
 
El valor numero es la proporción de la altura total que ocupa una letra minúscula X (conocido como el altura x). En otras palabras, una fuente puede
tener una altura total de 16 píxeles, pero la altura de las letras minúsculas X podría ser la mitad (8px), lo que da una relación de altura x de 0,5
(8 dividido por 16):

     p { font-size-adjust: 0.5; }
 
Mediante el uso ajuste de tamaño de fuente,puede asegurarse de que, independientemente de la fuente que se muestre, la altura x siempre tenga el mismo 
valor y la legibilidad no se vea afectada. Para ilustrar, considere el siguiente código:

     h1.adjusted { font-size-adjust: 0.517; }
     h1.impact { font-family: Impact, serif; }
 
Luego, en los siguientes tres h1 elementos, todos con los mismos valores para tamaño de fuente, Les aplico diferentes valores usando sus nombres de clase,
que puedes ver en este marcado:


     <h1>Of most excellent fancy</h1>
     <h1 class="impact">Of most excellent fancy</h1>
     <h1 class="adjusted impact">Of most excellent fancy</h1>

La primera h1 se representa en la fuente predeterminada Helvetica Neue, el segundo en Impact y el tercero también en Impact pero con el font-size-adjust
propiedad aplicada usando el valor 0,517, que es la altura x de Helvetica Neue. 

