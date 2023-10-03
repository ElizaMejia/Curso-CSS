# Pseudo - clases y Pseudo - elementos


La primera especificación CSS, CSS1, introdujo los conceptos de pseudo-clases y pseudo-elementos. Estos son selectores que actúan sobre la información, sobre 
elementos que se extienden o se  encuentran fuera de el árbol del documento. 
Una pseudo-clase diferencia entre los diferentes estados o tipos de un elemento; estos incluyen, entre otros, aquellos que proporcionan información sobre los
estados de los enlaces: :hover, :visited, :active, etcétera. 

Un pseudo-elemento proporciona acceso a la subparte de un elemento, que incluye aquellos pseudo-elementos que seleccionan  partes de nodos de texto; por 
ejemplo, first-line and :first-letter. 

La ventaja de tener más métodos para recorrer documentos debería ser clara: se requieren menos ganchos de estilo. Probablemente esté familiarizado con 
etiquetas como esta:

    <ul>
       <li>class="(1) first (2)odd"> (3)<span>L</span>orem ipsum</li>
       <li>Lorem ipsum</li>
       <li>class="odd">Lorem ipsum</li> 
       <li>class=(4) "last">Lorem ipsum</li> 
    </ul>

El marcado contiene nombres de clases para describir la posición de cada elemento en el árbol del documento: first  (1) y last (4) mostrar que “li”. 
Los elementos son los primeros y últimos hijos del elemento “ul”, y “odd”(2) se utiliza para  los impares elementos. Un “span” (3) se incluye alrededor de la 
primera letra de la inicial elemento.
Los nuevos métodos de CSS3 le permiten lograr los mismos resultados visuales sin enturbiar el marcado con clases innecesarias y elementos no semánticos, lo que
genera un código más limpio y fácil de mantener:

    <ul>
       <li>Lorem ipsum</li>
       <li>Lorem ipsum</li>
       <li>Lorem ipsum</li>
       <li>Lorem ipsum</li>
    </ul>
    
La otra gran ventaja de los nuevos selectores es que si se agregan nuevos elementos al marcado, no es necesario actualizar los nombres de las clases para
acomodarlos y al mismo tiempo mantener el orden. Este cambio acerca a CSS un gran paso hacia el logro de su objetivo declarado: la separación de contenido y 
presentación.


## Pseudo - clases estructurales

Una pseudo-clase proporciona una forma de seleccionar un elemento basándose en información que no está especificada en el árbol del documento. Hay varios 
subtipos disponibles, el más común de los cuales es el pseudo-clase estructural. Estos subtipos se utilizan para seleccionar elementos a los que no se puede
acceder mediante selectores simples.
 
Tomemos, por ejemplo, el siguiente marcado:

    <div>
       <p>Lorem ipsum.</p>
       <p>Dolor sit amet.</p>
    </div>
    
El primero de los dos pag elementos es el primer hijo de div elemento. Esto es obvio en el árbol del documento, pero el árbol del documento no proporciona 
ninguna información que le permita aplicar una regla solo a ese elemento. 

CSS2 introdujo:first-child pseudo-clase exactamente por esa razón:
 
    E:first-child {...}
    
Esta pseudo-clase le permite realizar una selección basada en información que existe pero que no se proporciona como atributo del elemento: el propósito exacto
de una pseudo-clase. Desde :first-child se introdujo en CSS2, ha sido la única pseudo-clase de este tipo. Pero CSS3 amplía enormemente el alcance con la 
introducción de 11 nuevas pseudo-clases estructurales.

## Las :nth-* pseudo-clases

Cuatro de las nuevas pseudo-clases se basan en un valor de recuento utilizado para encontrar la posición de un elemento en el árbol del documento; para este
recuento se utiliza la sintaxis:nth-*. Tenga en cuenta que he utilizado el asterisco aquí en lugar de varios valores diferentes, cada uno de los cuales 
presentaré a lo largo del resto de este capítulo.

La sintaxis básica de :nth-*pseudo-clases es bastante sencillo. 

    E:nth-*(n) {...}
    E:nth-*(2n) {...}
    E:nth-*(3n) {...}


El primer ejemplo utiliza el valor predeterminado n, entonces todos los elementos de tipo E sería seleccionado; en la práctica, esto es lo mismo que usar un 
selector de elementos simple. 
El siguiente ejemplo selecciona uno al otro E elemento, y el ejemplo final selecciona cada tercer elemento de tipo E.

También puedes utilizar los operadores matemáticos para más (+) y menos (-). 
Entonces 2n+1 selecciona cada múltiplo de dos más uno (1, 3, 5, etc.), y 3n-1 selecciona cada múltiplo de tres menos uno (2, 5, 8, etc.):

    E:nth-*(n+1) {...}
    E:nth-*(2n+1) {...}
    E:nth-*(3n-1) {...}
 
El primer ejemplo selecciona cada elemento de tipo E excepto en primera instancia; la cuenta para esto sería 2, 3, 4, 5, etc. 
El siguiente ejemplo selecciona cada número impar E elemento (1, 3, 5, etc.).
El último ejemplo, como se acaba de mencionar, selecciona elementos en la secuencia 2, 5, 8, etc.

Dos valores de palabras clave especiales, even y odd, también están disponibles; puedes usar estos para reemplazar 2n y 2n+1,respectivamente:

    E:nth-*(even) {...}
    E:nth-*(odd) {...}

Finalmente, también es aceptable usar On (eso es cero) como valor. No tiene ningún uso por sí solo, pero es muy útil cuando se combina con un operador
matemático, ya que permite identificar un único elemento sin que se repita. De hecho, por motivos de brevedad, sólo puede proporcionar el valor después del 
operador matemático. 

Por ejemplo, para seleccionar solo el tercer elemento en una lista de selección, ambos valores son válidos:

    E:nth-*(0n+3) {...}
    E:nth-*(3) {...}

## :nth-child() y :nth-of-type()

La mayoría de las nuevas pseudo-clases estructurales le permiten seleccionar elementos en función de su posición en el árbol del documento en relación con su
elemento principal (-child) o su clasificación (-of-type).

Los ejemplos más simples de estas pseudo-clases son: **nth-child() y :nth-of-type().**

La primera nth-child(), selecciona un elemento en función de su posición en un recuento del número total de hijos en su elemento padre; :nth-of-type() basa 
su recuento no en el total de hijos, sino sólo en aquellos del tipo de elemento especificado.

    (1)E:nth-child(n) {...} 
    (2)E:nth-of-type(n) {...} 
    (3)E:nth-child(2n) {...} 
    (4)E:nth-of-type(2n) {...} 


En este ejemplo, las reglas (1) y (2) son equivalentes porque el valor de conteo (n)se deja en el valor predeterminado; ambos simplemente seleccionan todos 
los elementos secundarios de tipo E. 
La diferencia se revela en los ejemplos posteriores: en 3, :nth-child(2n) selecciona todos los elementos del tipo E de un recuento que incluye a todos sus
hermanos pero solo cuando esos elementos son pares. 
En (4),en comparación, :nth-of-type(2n) selecciona todos los elementos pares del tipo E de un recuento que incluye sólo esos elementos.

**Resultado del Ejemplo 1, del archivo "Ejemplos_Capitulo4" anexado en la carpeta "Capitulo 4" del presente repositorio**

![Imagen ilustrando el capitulo 4](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo4/Imagenes/Ejemplo%201_C4.png)

## :nth-last-child() y :nth-last-of-type()

El :nth-last-child() y :nth-last-of-type() pseudo-clases aceptan la mismos argumentos que :nth-child() y :nth-of-type(),excepto que se cuentan desde el
último elemento, trabajando a la inversa. 


## :first-of-type, :last-child, y :last-of-type

:first-of-type es más específico y se aplica solo al elemento que es el primer hijo del tipo nombrado de su padre. También está disponible un par de 
pseudo-clases homólogas, :last-child and :last-of-type, que como habrás adivinado, selecciona el último elemento hijo o el último elemento hijo de ese tipo,
respectivamente, del padre.

**Resultado del Ejemplo 2, del archivo "Ejemplos_Capitulo4" anexado en la carpeta "Capitulo 4" del presente repositorio**

![Imagen ilustrando el capitulo 4](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo4/Imagenes/Ejemplo%202_C4.png)

**Resultado del Ejemplo 2.1, del archivo "Ejemplos_Capitulo4" anexado en la carpeta "Capitulo 4" del presente repositorio**

![Imagen ilustrando el capitulo 4](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo4/Imagenes/Ejemplo2.1_C4%20.png)

## :only-child y :only-of-type

Estas dos pseudo-clases se utilizan para seleccionar elementos en el árbol del documento que tienen un padre pero no tienen elementos hermanos (:only-child)
o ningún hermano del mismo tipo (:only-of-type). Como ocurre con muchas de las pseudo-clases anteriores, estas dos se superponen sustancialmente en función.

**Resultado del Ejemplo 3, del archivo "Ejemplos_Capitulo4" anexado en la carpeta "Capitulo 4" del presente repositorio**

![Imagen ilustrando el capitulo 4](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo4/Imagenes/Ejemplo3_C4.png)

# otras pseudoclases
Además de las pseudo-clases estructurales analizadas hasta ahora en este capítulo, CSS3 introduce una serie de pseudo-clases que le permiten seleccionar 
elementos basándose en otros criterios. Estos incluyen destinos de enlaces, elementos de la interfaz de usuario e incluso un selector inverso que permite 
la selección en función de lo que un elementono es.

## :target
En la Web, los sitios no sólo enlazan entre páginas sino que también proporcionan enlaces internos a elementos específicos. Un URI puede contener una referencia
a una identificación única o un ancla con nombre. 

    <h4 id="my_id">Lorem ipsum</h4>

Puedes consultarlo con este enlace:

    <a href="page.html#my_id">Lorem</a>

El :target a pseudo-clase le permite aplicar estilos al elemento cuando se ha seguido el URI de referencia. En este ejemplo, si desea aplicar estilos 
al h4 elemento cuando se sigue el URI, se utiliza:

    #my_id:target {...}

## :empty
La pseudo-clase :empty selecciona un elemento que no tiene hijos, incluidos los nodos de texto. 

## :root
La pseudo-clase :root selecciona el primer elemento en un árbol de documentos, lo cual solo es realmente útil si agrega una hoja de estilo a documentos XML; en HTML, la raíz siempre será la HTML elemento. Una pequeña ventaja de usar :root en HTML es que puedes usarlo para darle una mayor especificidad al HTML elemento, que podría ser útil si necesita anular el selector de tipo simple

## :not()
La pseudo-clase de negación :not() selecciona todos los elementos excepto los que se dan como valor de un argumento:

    E:not(F) {...}

Esta regla selecciona todos los hijos del elemento E excepto los del tipo F.

## UI Element States
Los elementos relacionados con formularios y entradas del usuario pueden tener varios estados; se pueden desactivar o comprobar

CSS3 tiene tres selectores de pseudoclases de estado de UI, que le permiten aplicar reglas a elementos según su estado actual:

    :checked {...}
    :disabled {...}
    :enabled {...}


**Resultado del Ejemplo 8, del archivo "Ejemplos_Capitulo4" anexado en la carpeta "Capitulo 4" del presente repositorio**

![Imagen ilustrando el capitulo 4](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo4/Imagenes/ejemplo8_C4.png)

## Pseudoclases de validación de restricciones
Bajo la validación de restricciones, un campo de formulario puede hacerse obligatorio mediante el uso del nuevo required atributo:

    <input type="text" required>
    
Puedes diseñar elementos dependiendo de si son obligatorios u opcionales usando sus pseudoclases homónimas:

    :required {...}
    :optional {...}

Cada campo del formulario puede estar en uno de dos estados de validación: válido o no válido. Si no se aplican restricciones específicas, ni por parte del navegador ni del autor, un campo de formulario es válido de forma predeterminada. Como antes, cada estado tiene una pseudoclase homónima:

    :valid {...}
    :invalid {...}
    
Finalmente, algunos elementos HTML5 pueden tener un rango de valores permitido, establecido mediante el mín y máximo atributos. Puede diseñar estos elementos dependiendo de si el valor actual está dentro o fuera del rango usando, una vez más, un par de pseudo-clases homónimas:

    :in-range {...}
    :out-of-range {...}

# Pseudo elementos

Al igual que las pseudo-clases, los pseudo-elementos proporcionan información que no se especifica en el árbol del documento. Pero mientras que las pseudo-clases utilizan condiciones "fantasmas", como la posición de un elemento en el árbol o su estado, los pseudo-elementos van más allá y le permiten aplicar estilos a elementos que no existen en absoluto en el árbol.

En CSS2, los cuatro pseudo-elementos son :first-line y :first-letter, que seleccionan subelementos en nodos de texto, y  :after and :before, que le permiten aplicar estilos al principio y al final de elementos existentes. CSS3 no introduce ningún pseudo-elemento nuevo, pero refina ligeramente las definiciones e introduce una nueva sintaxis para diferenciarlas de las pseudo-clases. En CSS3, los pseudoelementos tienen el prefijo dos puntos dobles (::), así:

    ::first-line {...}
    ::first-letter {...}
    ::after {...}
    ::before {...}

## El pseudo-elemento ::selection

Las primeras versiones del módulo Selectores CSS3 incluían la definición de un ::selection pseudo-elemento. Aunque se eliminó formalmente del módulo, se ha implementado bien en los navegadores de escritorio (menos en los navegadores móviles). ::selection se utiliza para aplicar reglas a un elemento que el usuario ha seleccionado en el navegador (por ejemplo, una parte de un nodo de texto):

     ::selection {...}
Sólo se puede aplicar un número limitado de propiedades ::selection : color, background-color y background shorthand (aunque no background-image). Usando ::selection, es posible hacer algo como:

    p::selection {
        background-color: black;
        color: white;
    }








