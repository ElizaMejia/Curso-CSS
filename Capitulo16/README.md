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

