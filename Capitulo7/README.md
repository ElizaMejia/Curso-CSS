# Múltiples columnas 

Aunque las pantallas de las computadoras de escritorio y portátiles se han vuelto más anchas en los últimos años, aún se estudia cómo las personas 
tienen dificultades para leer, largas líneas de texto. (Aproximadamente 65 a 75 caracteres (Por lo general, se considera una longitud cómoda de
lectura). Esta convención ha dado lugar a diseños restringidos y sitios web que no aprovechan las oportunidades que presentan las pantallas más anchas.

Durante años, las revistas y los periódicos han utilizado varias columnas para hacer fluir el contenido, abordando tanto el problema de las líneas de
texto largas como la forma de empaquetar una gran cantidad de textos en espacios limitados. Ahora, con la llegada del módulo de diseño de varias 
columnas en CSS3 (http://www.w3.org/TR/css3-multicol/), los sitios web también pueden aprovechar varias columnas.

El módulo de diseño de varias columnas actualmente tiene estado de recomendación candidata, lo que significa que el módulo se considera mayormente 
completo y está bien implementado en IE10+ y otros navegadores modernos, por lo que hay muchas oportunidades para experimentar con múltiples columnas.

## Métodos de diseño de columnas
Puede dividir su contenido en columnas usando dos métodos: ya sea de forma prescriptiva, estableciendo un número específico de columnas, 
o dinámicamente, especificando el ancho de las columnas y permitiendo que el navegador calcule cuántas columnas caben en el ancho del elemento 
principal.

### Columnas prescriptivas: recuento de columnas

La forma más sencilla de dividir su contenido en columnas distribuidas equitativamente es utilizar la propiedad recuento de columnas:

     E { column-count: columns; }
       
El elemento E es el padre del contenido que desea dividir, y el columns es un número entero que establece el número de columnas. Por ejemplo, para 
hacer fluir el contenido dentro de un div elemento en dos columnas, usaría:

     div { column-count: 2; }
       
Resultados del "Ejemplo 1", del documento Ejemplos_Capitulo7.css subido en el presente repositorio

# Imagen 1

### Columnas dinámicas: ancho de columna

El segundo método para dividir el contenido en columnas es quizás una mejor opción para diseños flexibles. En lugar de especificar el número de
columnas, utilice elancho de columna propiedad para especificar el ancho de cada columna, y el navegador llena el elemento principal con tantas 
columnas como puedan caber a lo largo de su ancho. La sintaxis es igual de sencilla:

     E { column-width: length; }

Al igual que conrecuento de columnas,E es el elemento principal del contenido que desea dividir en columnas, pero ancho de columna se diferencia en
que requiere una longitud: una unidad de longitud (como px o em) o un porcentaje. He aquí un ejemplo:

     div { column-width: 150px; }

Resultados del "Ejemplo 2", del documento Ejemplos_Capitulo7.css subido en el presente repositorio, se tiene un elemento con un nombre de clase
de columnas,que tiene 710 px de ancho; el contenido que contiene se distribuirá en columnas de 150 px de ancho, con el ancho de columna establecido 
en 150px, el navegador ha creado cuatro columnas para llenar el elemento principal y un espacio de 12 px entre cada columna, el ancho total llega a 
636 px, pero el algoritmo que crea las columnas es bastante inteligente y cambia el tamaño de las columnas automáticamente para que se ajusten mejor
al elemento principal. 
Utiliza 150px como mínimo valor, haciendo que cada columna sea más ancha hasta que el ancho total coincida con el de su principal; en este 
caso, cada columna cambia de tamaño a 168,5 px.

# Imagen 2

### Distribución variable de contenido entre columnas

De forma predeterminada, el contenido que fluye en varias columnas se equilibrará de la manera más equitativa posible entre las columnas, de modo que
ninguna columna sea más larga que las demás. Si el navegador no puede organizar el contenido de modo que haya el mismo número de líneas en cada 
columna, la última columna se acortará, como se muestra en la figura inferior.

# Imagen 3

Se puede ver que las tres columnas tienen el mismo número de líneas. Si se desea cambiar este comportamiento predeterminado, se puede hacer con la 
propiedad relleno de columna:

     E { column-fill: keyword; }

Esta propiedad tiene dos posibles valores de palabras clave: el valor predeterminado es balance, que intenta hacer que todas las columnas tengan la 
misma longitud, y la alternativa es auto,que llena las columnas secuencialmente.
El valor auto tiene efecto solo cuando el elemento principal tiene una altura fija. El contenido fluye hacia la primera columna para llenar la altura
y luego hacia la siguiente columna hasta que se llena, y así sucesivamente.

En la imagen inferior se puede ver un ejemplo de auto valor por relleno de columna; las dos primeras columnas tienen el mismo número de líneas y la
tercera tiene tres menos, ya que el texto simplemente fluye hacia las columnas sin que el navegador intente equilibrarlos.

# Imagen 4

### Combinando recuento de columnas y ancho de columnas

Puedes configurar ambas propiedades recuento de columnas y ancho de columna en un elemento, aunque al principio podría pensar que hacerlo crearía 
un conflicto. Sin embargo, se ha tenido en cuenta esta posibilidad: si ambas propiedades se aplican al mismo elemento, el valor de recuento de 
columnas actúa como máximo. 

Resultados del "Ejemplo 3", del documento Ejemplos_Capitulo7.css subido en el presente repositorio, se divide el texto en columnas de 150 px cada una,
a menos que eso cree tres o más columnas, en cuyo caso haga tres columnas con un ancho mínimo de 150 px.

# Imagen 5

Si se desea utilizar estas dos propiedades juntas, hay disponible una propiedad abreviada:

     E { columns: column-width column-count; }

Entonces, si usara los valores del resultado del Ejemplo 3 con esta propiedad abreviada, se vería así:

     div { columns: 150px 3; }
 
