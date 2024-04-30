# Diseño de cuadrícula

Recientemente, los navegadores han comenzado a implementar un sistema de diseño de cuadrícula CSS nativo. Este módulo proporciona una serie de propiedades diseñadas específicamente para crear cuadrículas en la pantalla, lo que significa que el desarrollador ya no tiene que hackearlas a partir de propiedades y comportamientos existentes.
La gama completa de propiedades en el módulo Diseño de cuadrícula es bastante extensa, por lo que me centraré en los aspectos más inmediatamente útiles y no me empantanaré en detalles que podrían resultar potencialmente confusos. Cuando sea apropiado, señalaré los puntos donde he omitido algún detalle.

## Terminología de cuadrícula

Los siguientes son los términos clave utilizados en el módulo Diseño de cuadrícula:

1. Contenedor de rejilla: El elemento contenedor que actúa como límite y establece las dimensiones de la cuadrícula.
2. Líneas de cuadrícula: Las líneas divisorias entre filas y columnas. Estas líneas son teóricas, no reales.
3. Pistas de cuadrícula: Un nombre abreviado para filas y columnas. Cada columna o fila creada en la cuadrícula se denominapista. Las pistas son los espacios entre líneas.
4. Celdas de cuadrícula: Cada intersección de una columna y una fila crea unacelúla. Son como celdas de una tabla.
5. Áreas de cuadrícula: Una celda o varias celdas que marcan el espacio en el queelemento de la cuadrículaserá puesto.
6. Elementos de la cuadrícula: Cada elemento hijo colocado en la cuadrícula.

Se crea una cuadrícula estableciendo primero una cantidad de líneas en el contenedor de la cuadrícula para crear una serie de pistas. Luego, los elementos de la cuadrícula se colocan en las pistas usando líneas como coordenadas para crear áreas, como se muestra en la imagen inferior

![Imagen 1 ilustrando el capitulo 17](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo17/Imagenes/C17/Imagen1_C17.png)

Las líneas de la cuadrícula son las líneas entre las celdas. Definen una serie de filas y columnas, que están numeradas para la ubicación de las coordenadas.

## Declarando y definiendo la grilla

El primer paso para crear una grilla es declarar el contenedor de rejilla,el elemento utilizado como base de la cuadrícula. Las dimensiones del contenedor de la cuadrícula son los límites de la cuadrícula y todas las propiedades de la cuadrícula se le aplican. Para declarar el contenedor de la grilla, use el mostrar propiedad con el nuevo valor red como esto:

     E { display: grid; }

Esta declaración crea un contenedor de cuadrícula a nivel de bloque. El siguiente paso es definir sus pistas (filas y columnas). Puede definir pistas en un cuadrícula explícita, con un número preciso de columnas y filas, o en un cuadrícula implícita,que se crea en relación con su contenido. También puedes combinar cuadrículas explícitas e implícitas.

## Crear cuadrículas explícitas estableciendo el tamaño de la pista

En una cuadrícula explícita, puede definir un número específico de pistas de cuadrícula estableciendo su tamaño mediante un par de propiedades:columnas-plantilla-cuadrícula y filas de plantilla de cuadrícula.El valor de cada propiedad es una lista de longitudes separadas por espacios, que establece el ancho de la columna o el alto de la fila. Por ejemplo, el siguiente fragmento de código crea una cuadrícula de tres columnas, donde la primera y la última columnas se establecen en el 20 por ciento del ancho del contenedor de la cuadrícula y la segunda en el 60 por ciento del ancho:

     E { grid-template-columns: 20% 60% 20%; }

Puede utilizar porcentajes o cualquier unidad de longitud, incluida la unidad de longitud de cuadrícula especializada llamada fracción (fr). Un fr equivale a una parte igual de cualquier longitud no asignada en una cuadrícula. En el siguiente codigo el contenedor de la cuadrícula tiene un valor de ancho de 600 px y tres columnas tienen cada una un ancho definido:


     E{
          display: grid;
          grid-template-columns: 100px 100px 200px;
          width: 600px;
      }

El ancho total de las columnas es 400 px, que es 200 px menos que el ancho del contenedor. En este caso, agregar una columna adicional de 1fr de ancho hace que esa columna sea tan ancha como todo el espacio restante, o 200px:

     E { grid-template-columns: 100px 100px 200px 1fr; }

Agregar otra columna del mismo ancho hace que ambas columnas tengan un ancho de 100 píxeles:

     E { grid-template-columns: 100px 100px 200px 1fr 1fr; }

Y hacer que una de esas columnas tenga 3fr de ancho significa que el ancho restante se divide en cuatro porciones iguales de 50px cada una, lo que hace que 1fr sea igual a 50px y 3fr sea igual a 150px:

     E { grid-template-columns: 100px 100px 200px 1fr 3fr; }

Volviendo al primer ejemplo de esta sección, podrías reemplazar los porcentajes con la unidad fr para lograr el mismo resultado:

     E { grid-template-columns: 1fr 3fr 1fr; }

En realidad, este código define tres líneas de cuadrícula, y una adicional se crea automáticamente al inicio de la dirección de escritura (que es la izquierda, en idiomas escritos de izquierda a derecha). Estas líneas crean tres pistas de cuadrícula verticales, o columnas, como se muestra en la imagen inferior.

![Imagen 2 ilustrando el capitulo 17](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo17/Imagenes/C17/Imagen2_C17.png)

Agrega filas de la misma manera. Por ejemplo, para crear tres filas con la primera de 60px de alto, la segunda con el valor de auto entonces es tan alto como su contenido, y el tercero 5em de alto, podrías usar este código:

     E { grid-template-rows: 60px auto 5em; }

La combinación de estas propiedades le permite definir completamente su cuadrícula. Por ejemplo, este código crea una cuadrícula básica de tres columnas y tres filas, para un total de nueve celdas:

     E{
         display: grid; 
         grid-template-columns: 1fr 3fr 1fr; 
         grid-template-rows: 60px auto 5em;
      }

Las columnas de esta cuadrícula se distribuyen en una proporción de 1:3:1, y las filas son de 60 px en la parte superior y 5 em en la parte inferior, con una fila central configurada en altura automática para acomodar su contenido.La cuadrícula resultante se parece a la imagen inferior.

![Imagen 3 ilustrando el capitulo 17](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo17/Imagenes/C17/Imagen3_C17.png)

## Colocar elementos en una cuadrícula explícita

Cada hijo inmediato de un contenedor de cuadrícula se convierte en un elemento de cuadrícula y debe colocarse en la cuadrícula. Para hacerlo, asigna al elemento una coordenada de celda usando un conjunto de propiedades de ubicación. El primero de ellos son inicio-columna-cuadrícula y inicio de fila de cuadrícula,y cada uno toma un único número entero como valor. Este número se refiere a la línea al inicio de una pista de cuadrícula (ya sea una columna o una fila), y las referencias de pista combinadas crean las coordenadas de una celda.
Por ejemplo, para colocar un elemento en la celda de la segunda fila de la segunda columna, utilice este código:


     F{
         grid-column-start: 2; 
         grid-row-start: 2;
      }

En la imagen inferior se muestra el resultado

![Imagen 4 ilustrando el capitulo 17](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo17/Imagenes/C17/Imagen4_C17.png)

El valor predeterminado tanto de inicio-columna-cuadrícula y inicio de fila de cuadrícula properties es 1, por lo que omitir cualquiera de los valores coloca el elemento en la primera fila o columna. Por ejemplo, el siguiente código coloca el elemento en la celda de la segunda columna de la primera fila:

     G { grid-column-start: 2; }

En la imagen inferior se muestra el resultado

![Imagen 5 ilustrando el capitulo 17](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo17/Imagenes/C17/Imagen5_C17.png)

De forma predeterminada, el elemento se coloca solo en la celda designada y cualquier contenido que no quepa desborda la celda verticalmente. Puede hacer que un elemento se expanda en tamaño para crear un área que cubra varias celdas en filas o columnas usando el final de columna de cuadrícula y final de fila de cuadrícula propiedades. Al igual que sus contra partes, estas propiedades toman un único valor de número entero, que designa la línea en la que debe terminar la celda. Por ejemplo, para que un elemento abarque tres filas, comenzando en la línea 1 y terminando en la 4, aquí está el código que usa :

     F{
         grid-row-start: 1;
         grid-row-end: 4;
      }

El elemento se coloca en la primera columna de forma predeterminada; comienza en la línea 1 y termina en la línea 4, lo que significa que abarca tres filas, como se muestra en la imagen inferior 

![Imagen 6 ilustrando el capitulo 17](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo17/Imagenes/C17/Imagen6_C17.png)

Como alternativa al método que se acaba de mostrar, puede utilizar el método durar palabra clave, seguida del número de pistas que abarca el elemento. La regla reescrita se ve así:

     F { grid-row-end: span 3; }

El durar la palabra clave se vuelve bastante útil cuando desea permanecer agnóstico acerca de la línea en la que comenzará un elemento de la cuadrícula, pero siempre desea que abarque el mismo número de columnas.

## Propiedades abreviadas de ubicación de cuadrícula

Escribir cuatro propiedades individuales para colocar un elemento en una cuadrícula parece algo detallado y, de hecho, las propiedades abreviadas harán que su código sea más conciso. Las propiedades en cuestión son columna de cuadrícula y fila de cuadrícula,y cada uno tiene la misma sintaxis. La primera,columna de cuadrícula,es corto para inicio-columna-cuadrícula y extremo de columna de cuadrícula, dividido por una barra; y lo mismo ocurre con fila de cuadrícula ser corto para inicio de fila de cuadrícula y final de fila de cuadrícula.
    

Si se aplican todas las propiedades individuales aplicadas al mismo elemento:

     F{
         grid-column-start: 2; 
         grid-column-end: 3;
         grid-row-start: 1; 
         grid-row-end: span 3;
      }

Usando las propiedades abreviadas, puedes escribirlas de una manera mucho más manejable:

     F{
         grid-column: 2 / 3; 
         grid-row: 1 / span 3;
      }

Es posible combinar todas estas instrucciones en una única regla abreviada.área de cuadrícula,que cubre las cuatro propiedades. Aquí está la sintaxis básica:

     F { grid-area: row-start / column-start / row-end / column-end; }

Insertar los valores apropiados nos da esta regla muy concisa, aunque posiblemente más difícil de leer:

     F { grid-area: 1 / 2 / span 3 / 3; }

## Repetir líneas de cuadrícula

Aunque las cuadrículas simples están bien para algunas situaciones del mundo real, las cuadrículas más complejas le brindan un control más preciso sobre el contenido. Tener más de 12 columnas en grandes cuadrículas tipográficas es bastante común y cada columna suele tener un canal(espacio vacío) entre él y su vecino. Definir una cuadrícula de 12 columnas podría ser repetitivo usando la sintaxis de Diseño de cuadrícula, como puedes ver en este código de ejemplo donde he mapeado 12 columnas de 1fr cada una, con un margen de 10px entre ellas:

     E { grid-template-columns: 1fr 10px 1fr 10px 1fr 10px 1fr 10px 1fr 10px 1fr 10px 1fr 10px 1fr 10px 1fr 10px 1fr 10px 1fr 10px 1fr; }

Puedes usar elrepetir() función para evitar este tipo de repetición cuando se utilizan cuadrículas más grandes. Esta función toma dos argumentos: un número entero que establece el número de repeticiones, seguido de un separador de coma y los valores de la línea de la cuadrícula que se repetirán. Por ejemplo, la siguiente regla crea la misma cuadrícula como en el ejemplo anterior, pero de forma mucho más concisa; define una pista que tiene 1fr de ancho y luego usa repetir()para crear un patrón de un canal de 10px seguido de una columna de 1fr once veces, para un total de 12 columnas de 1fr cada una.

     E { grid-template-columns: 1fr repeat(11, 10px 1fr); }

## Áreas de cuadrícula con nombre

Además de colocar elementos en una cuadrícula basada en coordenadas, también puede colocar elementos en áreas nombradas con el áreas de plantilla de cuadrícula propiedad. Con esta propiedad, puede dar nombres específicos a las áreas de la cuadrícula utilizando una serie de identificadores únicos en cadenas de texto. Aquí te mostraré lo que quiero decir:

     E{
         display: grid;
         grid-template-areas: 'a b c';
         grid-template-columns: repeat(3, 1fr);
      }

Ahora debería resultarle familiar dos de estas reglas: 
línea: establece el elemento para que actúe como un contenedor de cuadrícula y línea: crea tres columnas de 1fr cada una. Línea - utiliza el áreas de plantilla de cuadrícula propiedad para nombrar cada una de las columnas: cada identificador en la cadena separada por espacios (a,b, y C) coincide con las columnas, a su vez. Este resultado se muestra en la imagen inferior.

![Imagen 7 ilustrando el capitulo 17](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo17/Imagenes/C17/Imagen7_C17.png)


Para colocar un elemento usando un área con nombre, use el identificador del área como valor para el área de cuadrícula propiedad. Por ejemplo, para colocar un elemento en el medio (b) columna de mi cuadrícula de ejemplo, uso esto:

     F { grid-area: b; }

No es necesario utilizar caracteres individuales para nombrar áreas, como lo hice yo aquí; puedes usar cualquier cadena de caracteres, siempre que no contengan un espacio. Por ejemplo, para que su contenido sea más legible para los humanos, es posible que desee describir el propósito de cada área. He aquí un ejemplo:

     E { grid-template-areas: 'nav main side'; }
     F { grid-area: main; }

Cada cadena de identificadores representa una fila de la cuadrícula, por lo que para agregar una nueva fila, simplemente agrega una nueva cadena. Si utiliza el mismo identificador varias veces en la misma cadena, el área abarcará esa cantidad de columnas. Si utiliza el mismo identificador en la misma posición en diferentes filas, el área abarcará esa cantidad de filas. Puedes ver lo que quiero decir en el siguiente código; en la primera fila, se llama una columnana vegación y dos se llaman cabeza, entonces el cabeza el área abarcará dos columnas; la segunda fila también tiene una primera columna llamada navegación, entonces el navegación el área abarcará dos filas:


     E{
         display: grid;
         grid-template-areas:
            'nav head head'
            'nav main side';
         grid-template-columns: repeat(3, 1fr);
         grid-template-rows: 80px auto;
      }


Con este código, puede colocar elementos de la cuadrícula en áreas que abarcan varias pistas. En el siguiente fragmento, elemento F se coloca en el cabeza área, lo que significa que abarca la segunda y tercera columnas de la primera fila, y el elemento GRAMO
será colocado en el navegación área, haciendo que abarque la primera y segunda fila de la primera columna. Esto se muestra en la imagen inferior

     F { grid-area: head; } 
     G { grid-area: nav; }

![Imagen 8 ilustrando el capitulo 17](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo17/Imagenes/C17/Imagen8_C17.png)

     
## La taquigrafía de la plantilla de cuadrícula

Para evitar tener que escribir tres reglas separadas para definir una cuadrícula (plantilla-cuadricula- columnas, filas-plantilla-cuadrícula,y áreas de plantilla de cuadrícula),puedes usar elred- plantilla taquigrafía. Esta abreviatura simplifica la definición de columnas y filas, sin áreas con nombre. He aquí un ejemplo:

     E { grid-template: grid-template-columns / grid-template-rows; }

Para usar la propiedad con áreas de cuadrícula con nombre, agregue los identificadores después de la barra, como en este ejemplo:

     E { grid-template: repeat(3, 1fr) / 'nav head head'; }


Y si también desea definir alturas para las filas, puede agregar el valor de longitud de la fila después de cada cadena de identificador. Volvamos a ver la cuadrícula completa definida en la sección anterior:

     E{
          grid-template-areas:
            'nav head head'
            'nav main side';
          grid-template-columns: repeat(3, 1fr);
          grid-template-rows: 80px auto;
      }

Así es como se ve esa cuadrícula si se escribe usando el plantilla de cuadrícula taquigrafía:

     E{
         grid-template: repeat(3, 1fr) / 'nav head head' 80px 'nav main side'; 
      }


## Cuadrículas implícitas


Las cuadrículas implícitas se definen por su contenido, en lugar de los valores de longitud especificados de las cuadrículas explícitas. Cuando no te importa cuántas filas o columnas hay en tu cuadrícula, solo que cada elemento de la cuadrícula tenga un lugar, puedes usar el columnas-automáticas de cuadrícula y filas-automáticas de cuadrícula propiedades. Cada propiedad toma un valor único para especificar el ancho de la fila o columna. Por ejemplo, este código dice que cualquier columna creada debe tener 1fr de ancho y que cualquier fila nueva debe tener 80px:

     E{
         display: grid;
         grid-auto-columns: 1fr;
         grid-auto-rows: 80px;
      }

Ahora cualquier artículo con un columna de cuadrícula o fila de cuadrícula el valor se colocará en la cuadrícula, y la cuadrícula ajustará automáticamente su tamaño para acomodar los elementos, manteniendo todas las columnas y filas en el tamaño establecido. Por ejemplo, el siguiente código muestra un elemento de cuadrícula configurado para comenzar en la segunda columna de la primera fila y abarcar dos filas y dos columnas. La cuadrícula se expandirá para ajustarse a este elemento, como puede ver en la imagen inferior.

      F{
          grid-column: 2 / 4; 
          grid-row: 1 / span 2;
       }

![Imagen 9 ilustrando el capitulo 17](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo17/Imagenes/C17/Imagen9_C17.png)


## Elementos de la cuadrícula sin un lugar declarado
¿Qué sucede con los hijos del contenedor de la grilla que no tienen un lugar declarado en la grilla porque tampoco lo tienen? columna de cuadrícula o fila de cuadrícula ¿valores? Vuelven a los valores predeterminados de 1 y se apilan en la misma celda en la fila uno, columna uno.

Puede modificar este comportamiento predeterminado con el flujo automático de cuadrícula propiedad, que garantiza que cualquier elemento sin un lugar asignado se inserte en la cuadrícula donde hay espacio disponible. También puedes agregar un nivel de control sobre dónde se colocan. Aquí está la forma básica de esta regla:

     E { grid-auto-flow: keyword; }

La palabra clave puede ser columna o fila.Si utiliza columna,los elementos llenarán las celdas vacías en las columnas, moviéndose hacia abajo en la columna; si usas fila,los elementos llenarán filas vacías y se moverán a lo largo de la fila. Por ejemplo, en la imagen inferior, el contenedor de la izquierda tiene un flujo automático de cuadrícula valor de columna,de modo que los elementos que no se han colocado llenan las celdas de cada fila hacia abajo en la columna actual y luego saltan a la siguiente columna cuando la primera columna está llena. Por otro lado, el contenedor de la derecha tiene el valor de fila,por lo tanto, los elementos se colocan a lo largo de la fila hasta que se llena, momento en el que los elementos pasan a la segunda fila.

![Imagen 10 ilustrando el capitulo 17](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo17/Imagenes/C17/Imagen10_C17.png)

## Combinando grillas explícitas e implícitas

Cuando crea cuadrículas explícitas, es posible que el número de pistas de cuadrícula disponibles sea menor de lo que necesita para sus elementos. Supongamos que tiene una cuadrícula de tres columnas, pero se supone que un elemento de la cuadrícula abarca cuatro columnas:

     E { grid-template-columns: repeat(3, 1fr); } 
     F { grid-column: 1 / 5; }

En este caso, la cuadrícula se expandirá para contener las pistas creadas por el elemento; Se agregará una columna adicional a la cuadrícula, haciendo cuatro en total. Puede establecer el tamaño de estas pistas adicionales con el columnas-automáticas de cuadrícula y
filas-automáticas de cuadrícula propiedades.

El siguiente código crea una cuadrícula explícita de tres columnas y dos filas y permite cualquier elemento que exceda esta cuadrícula explícita agregando una cuadrícula implícita. Las columnas adicionales en la cuadrícula implícita se definen como 1fr de ancho, con filas adicionales de 80px de alto:

     E{
          grid-template-columns: repeat(3, 1fr);
          grid-template-rows: repeat(2, 80px);
          grid-auto-columns: 1fr; 
          grid-auto-rows: 80px;
       }

Ahora, cualquier elemento colocado en esta cuadrícula llenará un área que coincida con las dimensiones de la cuadrícula explícita.

## La cuadrícula Taquigrafía

Definir una cuadrícula con propiedades tanto explícitas como implícitas puede generar una gran lista de reglas. Por ejemplo, el siguiente código muestra un elemento con reglas para crear una cuadrícula explícita con áreas con nombre, así como propiedades de cuadrícula implícitas para permitir cualquier elemento que pueda extender la cuadrícula, lo que le brinda un total de seis reglas:

     E{
          grid-template-areas: 'a b b' 'a c d';
          grid-template-columns: repeat(3, 1fr); 
          grid-template-rows: 80px auto; 
          grid-auto-flow: row;
          grid-auto-columns: 1fr;
          grid-auto-rows: 80px;
       }


Afortunadamente, hay una propiedad abreviada disponible para esta lista de reglas. La taquigrafía se llamared-sin embargo, sólo puede usarlo para establecer cuadrículas explícitas o implícitas, no ambas. Para usarlo para establecer cuadrículas implícitas, use esta sintaxis:

     E { grid: grid-auto-flow grid-auto-columns / grid-auto-rows; }

Aquí está la abreviatura de las reglas de cuadrícula implícitas que se muestran en el código anterior:

     E { grid: row 1fr / 80px; }

El red la sintaxis para configurar cuadrículas explícitas es exactamente la misma que para el plantilla de cuadrícula propiedad que vio anteriormente en este capítulo. Siendo ese el caso, aquí está la abreviatura de las reglas de cuadrícula explícitas que se muestran al comienzo de esta sección:

     E { grid: repeat(3, 1fr) / 'a b b' 80px 'a c d'; }

## Orden de apilamiento del elemento de la cuadrícula

Al colocar elementos en una cuadrícula, a veces las áreas se super ponen. Para manejar tal eventualidad, puede crear un orden de apilamiento para definir la forma en que se apilan los elementos en la cuadrícula. Por ejemplo, se podría decir que los elementos que comienzan en la tercera fila deben apilarse encima de los elementos que comienzan en la primera fila, independientemente de su orden en el DOM.
Puede cambiar el orden de apilamiento con el índice z propiedad. Los elementos con mayor índice z el valor se apilará por encima de todos los demás. Por ejemplo, el siguiente marcado muestra dos div elementos que se convertirán en elementos de la cuadrícula:

     <div class="grid-item item-one">...</div>
     <div class="grid-item item-two">...</div>

Colocaré ambos elementos en la cuadrícula, pero al agregar el siguiente código me aseguro de que elemento uno se apilará encima de elemento dos haciendo que su columna y fila iniciales sean mayores que las de elemento dos:

     .item-one { 
                   grid-column: 2 / 4; 
                   grid-row: 2;
               }
               
     .item-two {
                   grid-column: 1 / 3;
                   grid-row: 1 / 3;
               }


Puede ver el resultado en el ejemplo a la izquierda de la imagen inferior:elemento uno está apilado arriba elemento dos. Pero si aumentas el índice z de elemento dos al igual que:

     .item-two { z-index: 2; }

verás eso elemento dos ahora está apilado arriba artículo uno,como se muestra a la derecha de la imagen inferior.

![Imagen 11 ilustrando el capitulo 17](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo17/Imagenes/C17/Imagen11_C17.png)

Un enfoque alternativo utiliza el orden propiedad, introducida como parte del módulo Flexbox. En grillas explícitas, esta propiedad actúa exactamente como índice z,cambiar el orden de apilamiento; Sin embargo, en las cuadrículas implícitas también cambia el orden en que se colocan los elementos en la cuadrícula.
Puedes ver esto en acción en la imagen inferior, donde he fluido tres cuadrículas. elementos (elemento uno,elemento dos, yelemento tres) en una cuadrícula con unflujo automático de cuadrícula valor de columna.En la cuadrícula de la izquierda, los elementos fluyen hacia la cuadrícula en el orden en que aparecen en el DOM, pero en la cuadrícula de la derecha, el orden de dos de los elementos cambia, como se muestra en la imagen inferior.

     .item-one { order: 2; } 
     .item-two { order: 3; }

![Imagen 12 ilustrando el capitulo 17](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo17/Imagenes/C17/Imagen12_C17.png)

## Sintaxis del diseño de cuadrícula de Internet Explorer}

Internet Explorer 10 fue el primer navegador en implementar las propiedades de diseño de cuadrícula, aunque con una sintaxis que desde entonces ha quedado obsoleta. Por lo tanto, puede replicar ciertos diseños de cuadrícula en IE10 e IE11 si tiene cuidado, pero con límites muy estrictos; el más notable es que solo puede crear cuadrículas explícitas.
Todas las propiedades de la cuadrícula de IE utilizan:EM-prefijo, al igual que el valor del mostrar propiedad:

     E { display: -ms-grid; }

Creas pistas con el -columnas-ms-gridy -filas-ms-cuadrícula propiedades, que son análogos acolumnas-plantilla-cuadrícula y filas de plantilla de cuadrícula.La diferencia está en la forma en que repites las líneas de seguimiento: cuando diseñas para IE, colocas los valores de ancho entre paréntesis, seguidos del número de repeticiones entre corchetes:

     E{
         -ms-grid-columns: (1fr)[3]; 
         -ms-grid-rows: (80px)[2];
      }


Los elementos de la cuadrícula se colocan con el -columna-ms-gridy -fila-cuadrícula-ms propiedades, que funcionan como columna de cuadrícula y fila de cuadrícula,pero solo permite un único valor numérico. Para distribuir elementos en varias celdas, debe usar:ms-gridcolumn-span y -ms-grid-fila-span para establecer el número de pistas que debe abarcar un elemento (como el durar palabra clave.)
Siendo ese el caso, las reglas aplicadas a los elementos E y F en este bloque de código son idénticos en función:

     E{
          -ms-grid-column: 1; 
          -ms-grid-column-span: 2; 
          -ms-grid-row: 2; 
          -ms-grid-row-span: 3;
       } 
