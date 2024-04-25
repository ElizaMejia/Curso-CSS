# Valores y dimensionamiento

## Unidades de longitud relativa
En CSS un unidad de longitud relativa es aquel cuyo valor es relativo a otra propiedad. Las dos unidades relativas en CSS2.1 son ellos,que se calcula a partir de tamaño de fuente propiedad de un elemento, y ex,que se calcula a partir de la altura x de

## Unidades relativas a la raíz
La primera unidad nueva introducida en CSS3 es la movimiento rápido del ojo. Se comporta como el ellos unidad de CSS2.1, pero en lugar de ser relativa a la tamaño de fuente valor del elemento actual, es relativo al tamaño de fuente valor de la raíz del documento (el HTML elemento).
A pesar de ellos es bastante útil, no está exento de inconvenientes, que se vuelven más evidentes cuando se anidan elementos. Para ilustrar el problema, usaré este marcado:

     <ul>
           <li>Western gorilla
                <ul>
                      <li>Western lowland gorilla</li>
                      <li>Cross River gorilla</li>
                </ul> 
           </li>
     </ul>

y esta sencilla regla de estilo: 

     li { font-size: 2em; }

Si supones que la raíz tamaño de fuente del documento es el valor predeterminado común del navegador de 16px, el primero li elemento tendrá un cálculo tamaño de fuente de 32px (16 multiplicado por 2). Pero el tamaño de fuente de lli los elementos anidados dentro del primero se calcularían en relación con el valor heredado, lo que los convertiría en 64 px (32 multiplicado por 2).
Aquí es donde el movimiento rápido del ojo La unidad se vuelve esencial. Aquí está el mismo código que el ejemplo anterior, solo que ahora usando el movimiento rápido del ojo en lugar de la el los unidad:

     li { font-size: 2rem; }

De nuevo, suponiendo una raíz tamaño de fuente de 16px, el primero li tiene un calculado tamaño de fuentede 32px. Esta vez, sin embargo, el tamaño de fuentede lo anidado li Los elementos también son relativos al valor raíz, al igual que su padre. Y no importa cuántas capas anidadas bajes, ese valor siempre es relativo a la raíz.

## Unidades relativas a la ventana gráfica

Al crear de manera responsiva, los desarrolladores tienden a usar valores porcentuales para los elementos de diseño, ya que se escalan con fluidez en el rango de diferentes tamaños de pantalla que los sitios web deben atender. Los porcentajes son útiles en un nivel superior, pero, como acaba de ver con el los unidades: puede tener dificultades al utilizar porcentajes con elementos anidados.


Este código ilustra el problema:

     <div class="parent">
            <div class="child">...</div>
     </div>

Ahora, imagina eso .padre es el 75 por ciento del ancho de la ventana gráfica y desea .niño ser el 65 por ciento del ancho de la ventana gráfica, no el ancho de su padre. Para hacer esto, debes dividir 65 entre 75, lo que te dará un resultado de 86,666 (por ciento). Este cálculo es bastante simple, pero cuanto más profundo es el anidamiento, más complejos se vuelven los cálculos.
Una mejor solución es utilizar las unidades relativas a la ventana gráfica de CSS3:vhyvw— que representan la altura y el ancho de la ventana gráfica, respectivamente. Cada unidad de valor representa el 1 por ciento de la dimensión apropiada de la ventana gráfica: 1vh es el 1 por ciento de la altura de la ventana gráfica y 1vw es el 1 por ciento del ancho de la ventana gráfica. Por ejemplo, el siguiente código crea un elemento que ocupa el 75 por ciento del ancho de la ventana gráfica y el 50 por ciento de su altura:

     E{
         height: 50vh;
         width: 75vw;
      }

La ventaja de utilizar estas unidades es que cuando los elementos están anidados, las unidades permanecen en relación con la ventana gráfica. Entonces, en el caso de mi ejemplo anterior, para hacer .niño 65 por ciento del ancho total de la ventana gráfica, simplemente haga esto:

     .child { width: 65vw; }

También está disponible otro par de unidades suplementarias:vmáx es equivalente a cualquiera que sea el mayor valor de vh y VW,y vmin es equivalente al valor menor. Por ejemplo, si la ventana gráfica fuera 480×640, la altura sería mayor, por lo que vmáx sería equivalente a vh,y vmin sería igual a vw. Cambie las dimensiones de la ventana gráfica (640 × 480) y vmáx y vmin invertir sus valores.
Entonces, si supone una ventana gráfica de 480 × 640, en el siguiente fragmento de código, elemento mi tiene 640 px de ancho y el elemento F tiene 480 px de ancho:

     E { width: 100vmax; } 
     F { width: 100vmin; }

La utilidad de vmáx y vmin consiste en garantizar que un elemento permanezca proporcional a la ventana gráfica independientemente de la orientación, lo que resulta útil cuando esa orientación puede cambiar fácilmente, como en un dispositivo móvil o tableta.


Internet Explorer 9 implementadovmincomo el vm unidad, pero ni ella ni IE10 soportan vmáx (el soporte se agregó en IE11). Muchos navegadores de teléfonos inteligentes más antiguos no admiten estas propiedades, aunque las versiones más nuevas (como iOS 6.0 y Android 4.4 y superiores) sí lo hacen (aunque a menudo sin soporte para vmáx,más notablemente en iOS al momento de escribir este artículo).

## Valores calculados

Uno de los mayores cambios en CSS3 radica en la forma en que se pueden declarar las longitudes. En CSS2.1, las longitudes son siempre un valor único más una unidad, y si se requieren cálculos (por ejemplo, restar el ancho de un borde del ancho total), el desarrollador tiene que hacer el cálculo. Pero en CSS3, el navegador realiza los cálculos.
Los cálculos CSS se realizan con elcalcular()función. Puede utilizar esta función en cualquier lugar donde utilice unidades de valores comunes: longitud, ángulo, número, etc. Toma como argumento cualquier expresión matemática que utilice esas unidades de valor comunes y cuatro operandos básicos: + (suma), - (resta), * (multiplicación) y / (división).

El calcular() la función es especialmente útil al mezclar unidades. Por ejemplo, podría crear una expresión para calcular el ancho de un elemento (como porcentaje) menos su borde (como el los)como esto:

     E{
         border: 10px;
         width: calc(75% - 2em);
      }

La suma y la resta se pueden realizar con cualquier unidad, pero cuando se usa la multiplicación, al menos un argumento a cada lado del operando debe ser un número sin unidades. En el caso de la división, el argumento después el operando debe ser un número sin unidades. A continuación se muestran ejemplos de cómo realizar tanto la multiplicación como la división:


     E{
        left: calc(5 * 10em); 
        width: (80% / 4);
      }

Puede utilizar paréntesis en expresiones para mostrar el orden computacional. Por ejemplo, el siguiente código muestra una expresión que realiza tres cálculos:

     E { height: calc(10% * 5 + 15% * 2); }

La expresión primero multiplica el 10 por ciento por 5 y luego lo suma al resultado del 15 por ciento multiplicado por 2. Esta configuración funciona bien, pero no es inmediatamente evidente cuando la miras y, dado un cálculo bastante complejo, podría ser realmente difícil. para entender de inmediato. La expresión se vuelve más fácil cuando se escribe entre paréntesis:

     E { height: calc((10% * 5) + (15% * 2)); }

También puedes usar anidados.calcular()funciones para lograr el mismo resultado. Al utilizar la multiplicación o división en una expresión, debe insertar un solo carácter de espacio en blanco alrededor del operando; si no lo hace, la expresión no será válida y la propiedad se ignorará. El siguiente código muestra una expresión escrita dos veces: la primera no es válida porque no tiene espacio alrededor del operando; el segundo tiene el formato correcto y, por tanto, es válido.

     E { border-width: calc(1em*10); } /* Invalid */ 
     E { border-width: calc(1em * 10); } /* Valid */

## Elementos de dimensionamiento

El tamaño de un elemento generalmente se establece usando el ancho o altura propiedades o sus máximo -y mín.-variantes, junto con un absoluto (píxeles),relativo (ellos),o valor porcentual. 
CSS3 introduce nuevas propiedades y valores destinados a proporcionar mayor flexibilidad adicional a través de una alternancia de modelo de caja y nuevos métodos de tamaño según el contenido.

## Tamaño de la caja

Durante muchos años, Internet Explorer implementó su modelo de caja en contravención de las especificaciones del W3C. El modelo del W3C dictaminó que el ancho El valor era el ancho del cuadro de contenido y que el relleno y los bordes eran adicionales. En el modelo de IE, por otro lado, el ancho el valor era igual al ancho total del elemento, incluido el relleno y los bordes. Considere estas reglas de estilo:

     E{
          border: 5px;
          padding: 10px;
          width: 100px;
      }

En el modelo IE, el cuadro de contenido tendría 70 px de ancho, mientras que en el modelo W3C, tendría 100 px completos.
Aunque el modelo estándar es más lógico, en ocasiones el modelo IE es más cómodo de utilizar. En CSS3, puede optar por utilizar el modelo IE con el tamaño de caja propiedad,la sintaxis es la siguiente:

     E { box-sizing: keyword; }

La palabra clave predeterminada es cuadro de contenido,lo que significa aplicar lo especificado ancho o alturaal cuadro de contenido únicamente, como en el modelo W3C. Por el contrario, el valor alternativo cuadro de borde significa que cualquier longitud especificada también debe incluir cualquier relleno y cuadros de borde.

La imagen inferior muestra la diferencia. El ejemplo superior utiliza el modelo de caja W3C, mientras que el inferior tiene el cuadro de borde valor aplicado. Como puede ver, el ancho total del ejemplo inferior es igual al cuadro de contenido del superior.

![Imagen 1 ilustrando el capitulo 16](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo16/Imagenes/C16/Imagen1_C16.png)

## Dimensionamiento intrínseco y extrínseco

Un desafío en el diseño web es que los elementos ignoran su contenido y el contexto en el que se utilizan; en otras palabras, sin JavaScript, un elemento no conoce las dimensiones de sus elementos secundarios o principales. CSS3 introduce un nuevo concepto que cambia un poco esa ecuación con la adición de intrínseco y extrínseco dimensionamiento. El tamaño intrínseco se basa en los elementos secundarios de un elemento y el tamaño extrínseco se basa en el tamaño del elemento principal.

Todos los modelos de tamaño intrínsecos y extrínsecos se aplican utilizando un valor de palabra clave en el ancho o altura propiedades (y sus min-ymax- variantes). Por ejemplo, esta lista muestra cómo se aplicaría un nuevo modelo de tamaño aancho:

     E { width: keyword; }

## Contenido máximo y contenido mínimo

Los primeros valores de palabras clave nuevos,contenido máximo y contenido mínimo,son valores intrínsecos que hacen que un elemento sea tan ancho o tan alto como el más grande (contenido máximo) o más pequeño (contenido mínimo)elemento de contenido (en texto, el ancho de la palabra más larga) que contiene. Considere este marcado de un imagen y pag elemento dentro de un contenedor div:

     <div>
           <img src="foo.png"> 
           <p>...</p>
     </div>
     
El elemento img tiene un ancho de 200px y el ancho del pages 300px. Si el div elemento tenía un ancho valor de contenido máximo, sería lo suficientemente ancho para contener el pag,y si tuviera un valor de contenido mínimo,sería lo suficientemente ancho para caber en el imagen y el texto en el pag envolvería.

Compare los resultados que se muestran en la imagen inferior, el elemento contenedor de la izquierda tiene elcontenido máximo valor aplicado, lo que lo hace tan ancho como el child más ancho (elpag),mientras que el de la derecha tiene contenido mínimo aplicado, lo que lo hace tan ancho como el child más estrecho (el imagen).

![Imagen 2 ilustrando el capitulo 16](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo16/Imagenes/C16/Imagen2_C16.png)

# Contenido adecuado

El siguiente valor de palabra clave intrínseco es potencialmente el más útil. Llamado contenido adecuado,dimensiona un elemento tal como lo hacen los elementos flotantes o las celdas de una tabla: un elemento se expandirá hasta ser lo suficientemente ancho como para contener su contenido, a menos que se alcance el ancho máximo del elemento, en cuyo caso, el contenido se ajustará.

En la imagen inferior se compara el efecto de contenido adecuado a contenido máximo y contenido mínimo.El cuadro en la parte superior izquierda tiene contenido adecuadose aplica y el contenido se ajusta cuando alcanza el límite del contenedor principal. Por el contrario, el cuadro en la parte superior derecha tiene contenido máximo aplicado, por lo que debería expandirse para adaptarse a su contenido; sin embargo, el cuadro ahora excede el ancho de su contenedor principal, que tiene un Desbordamiento valor de oculto,lo que significa que la caja está recortada.
El cuadro en la parte inferior izquierda también tiene contenido adecuado aplicado, por lo que el contenedor cambia de tamaño para adaptarse al ancho del contenido; el cuadro en la parte inferior derecha tiene contenido mínimo aplicado, por lo que el contenedor es sólo tan ancho como el imagen elemento y el contenido del texto se ajusta.

![Imagen 3 ilustrando el capitulo 16](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo16/Imagenes/C16/Imagen3_C16.png)
 
## Llenar

La palabra clave final en la especificación se llama llenar. (Pero en Firefox es disponible y en Chrome es relleno disponible!)Este valor extrínseco hace que un elemento llene todo el espacio disponible a lo largo de la altura o el ancho de su padre.
Digamos que quieres hacer un bloque en línea pag el elemento, con borde y relleno, se expande para ser tan ancho como su padre. Generalmente, aplicarías estas reglas:

     p{
          border-width: 0 0.5em; 
          display: inline-block; 
          padding: 0 1em;
          width: 100%;
      }

  
Sin embargo, como sabes, el ancho "real" de un elemento también incluye relleno y borde, por lo que, en este caso, el pag elemento desbordaría su padre. Una solución es utilizar el tamaño de caja propiedad, pero es posible que tenga buenas razones para mantener el modelo de caja estándar, por lo que una mejor alternativa es usar el tamaño intrínseco:

      p { width: fill; }

El resultado se muestra en la imagen inferior; el elemento de bloque en línea, con borde y relleno, cambia de tamaño para llenar el espacio disponible en su elemento principal.

![Imagen 4 ilustrando el capitulo 16](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo16/Imagenes/C16/Imagen4_C16.png)
