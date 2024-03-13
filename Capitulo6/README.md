# Tipos de Tipografías y Efectos

CSS3 amplía enormemente su conjunto de herramientas tipográficas al introducir una variedad de funciones nuevas y actualizadas en el módulo de texto.
La principal de estas nuevas características es la capacidad de agregar sombras al texto. Aunque esta adición no suena particularmente revolucionaria (los tipógrafos impresos han estado usando sombras durante mucho tiempo), la nueva sintaxis es lo suficientemente flexible como para permitir algunos efectos muy agradables. Una característica similar es el contorno de texto (o trazo de texto), que, aunque no se implementa ampliamente, aumenta la variedad de opciones disponibles al crear titulares decorativos. Además de estos, hay algunos efectos menos llamativos pero que pueden hacer maravillas con la legibilidad de su texto.

## Comprensión de ejes y coordenadas

Un concepto de sintaxis que es nuevo en CSS3 es el de eje(o ejes cuando tienes más de   uno). 

CSS utiliza el sistema de coordenadas Cartesianas, que consta de dos líneas, una horizontal y otra vertical, que se cruzan formando un ángulo recto. Cada una de estas líneas es un eje: La línea horizontal se conoce como eje x, y la línea vertical se conoce como eje y. El punto donde se unen las dos rectas se llama origen, se observa en la imagen inferior.

![Imagen 1 ilustrando el capitulo 6](https://github.com/ElizaMejia/Curso-CSS/blob/main/Imagenes/C6/Imagen1_C6.png)

Para los elementos en pantalla, mide las longitudes de estos ejes en píxeles. Los ejes y el origen están superpuestos en una cuadrícula. Imaginemos que cada cuadrado corresponde a un solo píxel. También notarás etiquetas positivas (+) y negativas (-) en cada extremo de cada eje; estos le indican que la distancia desde el origen se medirá positiva o negativamente en esta   dirección.

Las coordenadas son un par de valores, uno para cada eje, que indican la distancia desde el origen. El origen tiene coordenadas (0, 0). Por ejemplo, dadas las coordenadas (3, 4), encontraría el punto moviendo 3 píxeles a lo largo de la X-eje, y 4 píxeles a lo largo del y-eje.

En CSS, todos los elementos tienen una altura y un ancho, cada uno de los cuales es un número establecido de píxeles de largo (incluso cuando se usan otras unidades de longitud como un porcentaje). La altura y el ancho juntos crean una cuadrícula de píxeles; por ejemplo, un elemento que tiene un tamaño de 10 px por 10 px tiene una cuadrícula de píxeles de 100 px. Si considera que el origen del elemento está en la esquina superior izquierda, entonces los dos valores  posicionales para propiedades como posición de fondo corresponden exactamente a la -X y -Y coordenadas.

## Aplicar efectos dimensionales: texto-sombra

La posición de la sombra se establece usando el X y Ycoordenadas. La forma más simple de sintaxis acepta dos valores: X para establecer la distancia  horizontal desde el texto (conocida como desplazamiento x) y Y para establecer la distancia vertical (la desplazamiento y):

     E { text-shadow: x y; }
     
De forma predeterminada, la sombra tendrá el color que heredó de su padre (generalmente negro), por lo que si desea especificar un color diferente, deberá proporcionar un valor para eso, por ejemplo:

    E { text-shadow: x y color; }
    
Resultados del Ejemplo 1, del documento Ejemplos_Capitulo6.css subido en el presente repositorio

![Imagen 2 ilustrando el capitulo 6](https://github.com/ElizaMejia/Curso-CSS/blob/main/Imagenes/C6/Imagen2_C6.png)

No está limitado a números enteros positivos como valores de compensación; puedes usar tanto 0 (cero) como números negativos para obtener diferentes efectos. 

Resultados del Ejemplo 2, del documento Ejemplos_Capitulo6.css subido en el presente repositorio

![Imagen 3 ilustrando el capitulo 6](https://github.com/ElizaMejia/Curso-CSS/blob/main/Imagenes/C6/Imagen3_C6.png)

La propiedad también tiene una cuarta opción: radio de desenfoque. Esta opción establece el alcance del efecto de desenfoque en la sombra y debe usarse después de los valores de desplazamiento:

    E { text-shadow: x y blur-radius color; }
    
El valor del radio de desenfoque es, al igual que los dos valores de desplazamiento, también un número entero con una unidad de longitud; cuanto mayor sea el valor, más amplio (y más claro) será el desenfoque. Si no se proporciona ningún valor, se supone que el radio de desenfoque es 0. 

Resultados del Ejemplo 3, del documento Ejemplos_Capitulo6.css subido en el presente repositorio

![Imagen 4 ilustrando el capitulo 6](https://github.com/ElizaMejia/Curso-CSS/blob/main/Imagenes/C6/Imagen4_C6.png)

## Múltiples sombras

No tienes que limitarte a una sola sombra. La sintaxis de sombras admite la adición de múltiples sombras a un nodo de texto. Simplemente proporcione valores adicionales a la propiedad, usando comas para separarlos, así:

    E { text-shadow: value, value, value; }
    
Las sombras se aplican en el orden en que proporciona los valores. 

Resultados del Ejemplo 4, del documento Ejemplos_Capitulo6.css subido en el presente repositorio

![Imagen 5 ilustrando el capitulo 6](https://github.com/ElizaMejia/Curso-CSS/blob/main/Imagenes/C6/Imagen5_C6.png)

## Restringir el desbordamiento

En determinadas circunstancias (tal vez en dispositivos móviles donde el espacio de la pantalla es limitado) es posible que desee restringir el texto a una sola línea y un ancho fijo, tal vez al mostrar una lista de enlaces a otras páginas, donde no desea que el texto del enlace se muestre. envolver en varias líneas. 

Una nueva propiedad llamadad esbordamiento de texto está disponible en CSS3 solo para esas circunstancias. 

    E { text-overflow: keyword; }
    
Los valores de palabras clave permitidos son acortar y elipsis. El valor predeterminado es acortar, que actúa de la manera que acabo de describir: su texto se recorta en el punto donde sale del elemento contenedor. Pero el nuevo valor que es realmente interesante es elipsis, que reemplaza el último carácter completo o parcial antes del desbordamiento con un carácter de puntos suspensivos, el que parece tres   puntos (...).

Resultados del Ejemplo 5, del documento Ejemplos_Capitulo6.css subido en el presente repositorio

![Imagen 6 ilustrando el capitulo 6](https://github.com/ElizaMejia/Curso-CSS/blob/main/Imagenes/C6/Imagen6_C6.png)

## Alinear texto

La propiedad de texto alineado existe desde hace mucho tiempo, pero CSS3 le agrega dos nuevos valores:comenzar y fin. Para las personas que leen de izquierda a derecha, son equivalentes a los valores izquierda y derecha (respectivamente). Sin embargo, su verdadera utilidad está en sitios internacionalizados que también pueden usar texto de derecha a izquierda. Puede utilizar estos nuevos valores en la mayoría de los navegadores modernos, a excepción de Internet Explorer.
Lo nuevo de CSS3 es la propiedad alineación-texto, que le permite establecer la alineación de la última (o única) línea de texto en un bloque justificado. Esta propiedad acepta los mismos valores quetexto alineado:

    E { text-align-last: keyword; }

## Control de envoltura de línea

Un problema que se encuentra con frecuencia al trabajar con texto dinámico es el ajuste de líneas en lugares inapropiados.  

### Rompiendo palabras

La primera propiedad es ajuste de línea, que especifica si el navegador puede dividir palabras largas para que encajen en el elemento principal. La sintaxis es simple:

    E { word-wrap: keyword; }


Esta propiedad permite los valores de palabras clave normal o palabra de ruptura. El primero permite que las líneas se rompan solo entre palabras (a menos que se especifique lo contrario en el marcado) y el segundo permite que una palabra se rompa si es necesario para evitar el desbordamiento del elemento principal.

Resultados del Ejemplo 7, del documento Ejemplos_Capitulo6.css subido en el presente repositorio,el bloque de la izquierda no utiliza ajuste de palabras y el bloque de la derecha sí.

![Imagen 7 ilustrando el capitulo 6](https://github.com/ElizaMejia/Curso-CSS/blob/main/Imagenes/C6/Imagen7_C6.png)

### Separar palabras con guiones

Si prefiere una opción adicional para dividir palabras en varias líneas, puede utilizar la separación de palabras. Durante mucho tiempo, un estándar de impresión, los guiones indican dónde ocurre la ruptura, en una palabra. Puede separar su texto con guiones ya en HTML, utilizando la entidad de símbolo de separación de guiones. 
CSS3 hace esto algo más fácil a través de la propiedad de guiones:

    E { hyphens: keyword; }

Esta propiedad tiene tres posibles valores de palabras clave: manual separa palabras con guiones sólo cuando existe una sugerencia de separación de palabras en el marcado, es decir, utilizando el símbolo de separación de palabras suave mencionado en el párrafo anterior; auto separa palabras con guiones en un punto apropiado incluso si no hay sugerencias de separación de palabras; y ninguno nunca separa palabras con guiones, incluso si hay sugerencias presentes.

En la imagen inferior se puede ver un ejemplo, el párrafo de la izquierda no tiene separación de palabras, mientras que el párrafo de la derecha tiene un valor de auto; El navegador ha separado la palabra “conversaciones” (resaltada) con guiones y la ha dividido en dos líneas.

![Imagen 8 ilustrando el capitulo 6](https://github.com/ElizaMejia/Curso-CSS/blob/main/Imagenes/C6/Imagen8_C6.png)

### Cambiar el tamaño de los elementos

Otra propiedad nueva que es útil para elementos cuyo contenido es más ancho que su contenedor es la propiedad cambiar el tamaño. Esta propiedad le permite controlar las dimensiones de un elemento al proporcionar un controlador con el que puede arrastrar el elemento a un tamaño diferente.
 
La propiedad tiene la siguiente sintaxis:

    E { resize: keyword; }

Resultados del Ejemplo 8, del documento Ejemplos_Capitulo6.css subido en el presente repositorio, se muestra un elemento con el valor de ambos sobre la propiedad de cambiar el tamaño.

![Imagen 9 ilustrando el capitulo 6](https://github.com/ElizaMejia/Curso-CSS/blob/main/Imagenes/C6/Imagen8_C6.png)
