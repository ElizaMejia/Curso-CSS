# Diseño de caja flexible

A medida que CSS ha madurado y los navegadores se han vuelto más potentes, se ha propuesto una nueva gama de enfoques de diseño alternativos.
El más implementado se llama Diseño de caja flexible (o Caja flexible), hace que los elementos cambien de tamaño de manera flexible para adaptarse mejor al espacio disponible, sin necesidad de flotadores, posicionamiento o cálculos complejos.
Aunque ciertamente puedes crear diseños de páginas completas con Flexbox, es más adecuado para trabajar con elementos de interfaz y componentes más pequeños, es decir si está creando una interfaz de usuario o una aplicación (especialmente una aplicación con muchos botones, elementos de formulario o elementos interactivos), regiones), Flexbox le resultará extremadamente útil.

## Declarando el modelo de caja flexible

El primer paso para usar Flexbox es crear el contenedor flexible: el elemento principal que creará un nuevo contexto de formato para su contenido. Para declarar un contenedor flexible, simplemente use un nuevo valor para el mostrar propiedad:

E { display: flex; }

Esto crea un contenedor flexible a nivel de bloque; puedes usar la alternativa flexible en línea valor si prefiere un contenedor de nivel en línea.
Ahora puedes agregara rtículos flexibles al contenedor flexible. Un elemento flexible es cualquier elemento secundario del contenedor flexible, que está sujeto al contexto de formato creado por el contenedor. Por ejemplo, en el siguiente código si #envasese establece como contenedor flexible, los dos elementos secundarios se convertirán en elementos flexibles:

<div id="container">
  <div id="a">...</div>
  <div id="b">...</div>
</div>

En la figura inferior observe que los dos elementos tienen el mismo ancho y están dispuestos uno al lado del otro, sin necesidad de utilizar flotadores ni propiedades de posicionamiento. De forma predeterminada, los elementos flexibles se disponen en la dirección del texto del documento, es decir, de izquierda a derecha para idiomas como el inglés, de derecha a izquierda para idiomas como el árabe (especificado con el directorio atributo HTML o dirección propiedad CSS), y de arriba a abajo para idiomas como el japonés (configurado con eldirección del texto propiedad CSS, pero aún no es ampliamente compatible).

# Imagen 1
Para modificar la dirección de diseño predeterminada, puede utilizar el dirección flexible propiedad en el contenedor. El valor predeterminado fila dispone los elementos en una fila, mientras que un valor de columnalos dispone de arriba a abajo en una columna.

E{
display: flex; 
flex-direction: column;
}


## Alineación de caja flexible

Flexbox utiliza dos ejes para la alineación. Como se muestra en la imagen inferior, el eje principalva en la dirección en la que se colocan los elementos, de izquierda a derecha o de arriba a abajo. Cuando el valor de dirección flexible es fila,el eje principal es horizontal; cuando es columna,el eje principal es vertical. El eje transversal es la recta que corre perpendicular al eje principal: es vertical cuando la dirección es fila y horizontal cuando es columna.

# Imagen 2

Cuando se trata de contenedores y elementos flexibles, a menudo verá puntos denominados inicio y final de los ejes. Debido a que los ejes flexibles se pueden invertir (de arriba a abajo o de abajo hacia arriba, y de izquierda a derecha o de derecha a izquierda), se utilizan inicio y fin en lugar de direcciones relativas para evitar confusiones. 

Por ejemplo, cuando el eje principal es horizontal y la dirección es de izquierda a derecha, el inicio del eje principal es la izquierda y el final es la derecha; pero si el eje principal es vertical, el inicio del eje principal está en la parte superior y el final está en la parte inferior (o viceversa si se invierte).

## Invertir el orden del contenido

Una de las grandes capacidades de Flexbox es que puede cambiar rápidamente el orden en que se muestran los elementos, independientemente de su orden en el DOM. Por ejemplo, la imagen inferior muestra dos elementos dispuestos en una fila, en el orden en que se declaran en el DOM. ¿Qué pasa si quieres cambiar su orden?

# Image3 

Puedes hacer esto rápidamente con el dirección flexible propiedad, usando el valor fila inversa para invertir el orden en el que se muestran los elementos flexibles, como se muestra aquí. (Elcolumna-inversa El valor de la propiedad invierte el orden de los elementos flexibles que se muestran verticalmente en las columnas).

E { flex-direction: row-reverse; }

Debido a que invertir direcciones como esta también invierte la dirección del eje, en el caso de fila inversa,el inicio del eje está a la izquierda y el final a la derecha. En el caso de columna inversa,el comienzo está en la parte inferior y el final está en la parte superior.

## Reordenar completamente el contenido

Puede crear patrones de pedidos personalizados con el orden propiedad. La propiedad orden se aplica a los elementos flexibles (no a su contenedor). El valor de la propiedad es un número que crea un grupo ordinal que agrupa elementos con el mismo valor y los ordena por su grupo ordinal: todos los elementos del grupo con el número más bajo van primero, luego todos los elementos del segundo grupo con el número más bajo, y así sucesivamente. Todos los elementos sin un valor declarado se muestran primero porque tienen el valor predeterminado de 0.
Los elementos con el mismo número de grupo ordinal se agrupan en el orden en que aparecen en el DOM. Por ejemplo, considere cuatro elementos flexibles:


<div id="container">
               <div id="a">...</div>
               <div id="b">...</div>
               <div id="c">...</div>
               <div id="d">...</div>
</div>

Si no se establecen valores explícitos y si dirección flexibleno se invierte, los elementos secundarios se muestran en el orden en que aparecen en el DOM: A, B, C, y D.Pero reordenémoslos usando diferentes valores en el orden propiedad:

#a { order: 2; }
#b, #d { order: 3; }
#c { order: 1; }

Con estas reglas aplicadas, el orden en el que se presentan los elementos es: #c, #a, #b, #d. Artículo #C viene primero porque tiene el número de grupo ordinal más bajo, seguido de #a con el siguiente número más alto, entonces #b y
#d-ambos están en el grupo ordinal 3. No de artículo d viene al final porque viene más tarde en el orden DOM.

La imagen inferior muestra el resultado, observe que los artículos #C y #a comparten los mismos colores de fondo, al igual que
# b y #d.

# Imagen4

.flex-item:nth-child(even) { background-color: gray; }

Pero recuerda que los elementos sólo han cambiado de orden visualmente; conservan el mismo orden en el marcado, por lo que :enésimo niño() aplica el fondo gris a los elementos que deben estar numerados pares, es decir, # by #d.

## Añadiendo flexibilidad

Al utilizar Flexbox, es casi seguro que encontrará situaciones en las que las longitudes combinadas de los elementos flexibles a lo largo del eje principal sean mayores o menores que el ancho del contenedor flexible. Cuando esto sucede, entra en juego la parte “flexible” de Flexbox. Varias propiedades permiten que los elementos flexibles crezcan o se encojan para llenar su contenedor. 

### La propiedad de crecimiento flexible

Digamos que tiene un contenedor flexible de 600 px de ancho que contiene tres elementos flexibles. Cada uno tiene 150 px de ancho, lo que hace un ancho combinado de 450 px. La diferencia entre el ancho del contenedor y el ancho combinado de los elementos deja un espacio vacío de 150 px (es decir, 600 − 450) al final de los elementos, como se muestra en la imagen inferior.

# Imagen 5

Para expandir los elementos para llenar el contenedor, puede usar elcrecimiento flexible propiedad:

.flex-item { flex-grow: 1; }

La propiedad de el valor de la crecimiento flexible es básicamente una proporción que se usa para distribuir el espacio vacío entre los elementos flexibles para que se expandan. En este caso, utilicé una proporción de 1:1:1 para dividir los 150 píxeles vacíos en partes iguales entre los tres elementos flexibles. Debido a que 150 dividido por 3 es 50, cada elemento se expande en 50 px, lo que hace que su ancho total sea igual al ancho del contenedor, como se muestra en la imagen infrior.

# Imagen 6

También puede proporcionar diferentes valores para ajustar la relación de distribución. Por ejemplo, para hacer #b ocupa más ancho del contenedor que los otros dos elementos, puede establecer un valor de 3 para #b:

#b { flex-grow: 3; }

Ahora los 150 píxeles se redistribuirán utilizando la proporción 1:3:1, por lo que por cada píxel distribuido en #a y #c, #b recibirá tres. Como resultado #a y
# C cada uno se expandirá a 180 px de ancho, mientras que #b tendrá 240 px de ancho como se muestra en la imagen inferior.

# Imagen 7

Porque el valor predeterminado paracrecimiento flexible es 0 (cero), los elementos flexibles mantendrán su ancho y no se expandirán para llenar el contenedor a menos que se indique explícitamente que lo hagan.

      

### La propiedad flex-shrink

Tal como crecimiento flexiblese utiliza para expandir elementos flexibles para llenar su contenedor,flex-contraíble se utiliza para encoger elementos. Por ejemplo, revisemos nuestro contenedor flexible de la sección anterior con los elementos #a, #b,y #C; Solo en este caso, haremos que cada elemento tenga 300 píxeles de ancho. Ahora el ancho total de los tres elementos es de 900 px, lo que excede el ancho de 600 px del padre en 300 px.
Para reducir estos elementos para que quepan dentro del ancho del contenedor, puede usar el flex-contraíble propiedad:

.flex-item { flex-shrink: 1; }

El flex-contraíble la propiedad funciona como crecimiento flexible pero en dirección opuesta. Por ejemplo, un valor de 1 (el valor predeterminado) reduce cada elemento en la misma proporción: cada uno en 100 px (300 dividido por 3). Los elementos resultantes tendrán 200 px cada uno, para un total de 600 px, que coincide con el ancho del contenedor.
Como crecimiento flexible,diferentes valores cambian la relación de distribución. Por ejemplo, si usa un valor de 3 para el artículo #b,su ancho se reduce en tres píxeles por cada reducción de un píxel de los otros dos elementos.

#b { flex-shrink: 3; }

Los números más altos reducen los elementos en un factor mayor. En este ejemplo, por cada píxel eliminado del ancho de #a y #C,tres son eliminados de #b.Como puede ver en la imagen inferior, #a y #C tienen 240 px de ancho, mientras que #b Tiene solo 120 px, que es más estrecho que su ancho original.

# Imagen 8

### La propiedad de base flexible

El ancho de los elementos flexibles se puede establecer según el contenido que contienen o mediante una configuración explícita.ancho valor, y cualquier crecimiento o contracción se calcula a partir de ese ancho de base. Para cambiar cómo se calcula el ajuste de ancho, puede establecer un base flexible valor de un elemento. Esta propiedad toma como valor una unidad de longitud. He aquí un ejemplo:

.flex-item { flex-basis: 100px; }

Cuando base flexible se aplica, cualquier existente ancho el valor se ignora y el valor que especifique para el base flexible se utiliza para calcular el ajuste. Por ejemplo, en las dos secciones anteriores, el ancho El valor de 150px se ignora y todo crecimiento o reducción se basa en el base flexible valor de 100px. Podrías agregar el base flexiblevalor de 100px a #b en un ejemplo anterior es asi:

.child-item {
    flex-grow: 1;
    width: 150px;
}
#b {
    flex-basis: 100px;
    flex-grow: 3;
}

Ahora el espacio vacío en el contenedor se redistribuirá usando la proporción 1:3:1, lo que significa que, según el ancho valores, #a y #C se expandiría en 30px cada uno y #b por 90px. debido a la base flexible valor, sin embargo, que la distribución del espacio se realiza como si #b tenía un ancho de 100px, no el especificado ancho valor de 150px.

Al principio parece ilógico que #b termina siendo más ancho que sus hermanos a pesar de tener un ancho menor establecido por su base flexible valor. La razón es que ahora hay un ancho adicional de 200 px (el ancho combinado de los elementos flexibles es de 400 px; el principal es de 600 px). Estos 200 se redistribuyen entre las tres cajas utilizando la proporción 1:3:1. A pesar de #b comienza con 100 px de ancho, recibe 120 px del espacio libre, mientras que #a y #C recibir 40px.
Como resultado, #a y #C termina con 190 px de ancho y #b tiene 220 px de ancho. Compare el resultado que se muestra en la imagen 7 con la imagen inferior para ver la diferencia.

# Imagen 9

### La taquigrafía flexible

Como ocurre con muchas propiedades, la doblar-*la familia tiene una propiedad abreviada llamada doblar.Los valores que toma son, en orden,flex-crecer, flex-reducir,y base flexible. Considere este ejemplo:

E { flex: 1 2 150px; }

Aquí, elemento mi tiene un crecimiento flexible valor de 1 y aflex-contraíble valor de 2. El valor utilizado se elige en función del ancho de los elementos flexibles en comparación con su contenedor flexible; donde los artículos flexibles no llenan su contenedor, el crecimiento flexible Se utiliza el valor, y cuando los elementos flexibles exceden su contenedor, el valor flex-contraíble entra en juego. El valor final, 150px, es el base flexible valor.

## Alineación dentro del contenedor

Cuando tenga elementos con dimensiones fijas dentro de un contenedor flexible, probablemente tendrá espacio vacío a lo largo de uno o ambos ejes. Por ejemplo, en la imagen 5, tres elementos flexibles de 150 px de ancho cada uno no llenaron el ancho de su contenedor de 600 px. Cuando este sea el caso, puedes alinear los elementos dentro del contenedor para aprovechar mejor el espacio disponible.

### Alineación horizontal con justificación de contenido

Afortunadamente, Flexbox ofrece un control estricto sobre la alineación y la ubicación, lo que le permite redistribuir el espacio no utilizado con el justificar-contenido propiedad. Esta propiedad se aplica al contenedor flexible y acepta una serie de valores de palabras clave que se aplican de manera diferente dependiendo de la dirección del padre flexible (fila, columna, fila invertida, etc.):

.flex-container { justify-content: keyword; }

El valor predeterminado es inicio flexible,que alinea todos los elementos flexibles a la izquierda del padre con el espacio no utilizado que ocupa el ancho restante a la derecha. Los valores alternativos son los siguientes:

1. extremo flexible,que alinea los elementos a la derecha del contenedor con el espacio no utilizado a la izquierda
2. centro,que distribuye el espacio no utilizado a ambos lados de todos los artículos, centrando los artículos en el contenedor
3. espacio entre,que agrega una cantidad igual de espacio entre cada elemento pero ninguno antes del primero o después del último elemento
4. espacio alrededor,lo que pone una cantidad igual de espacio en ambos lados de cada elemento

   
El siguiente código muestra algunos valores diferentes para fines de comparación, y los resultados se muestran en la figuraa posterior.
  
.container-a { justify-content: flex-start; }
.container-b { justify-content: center; }
.container-c { justify-content: space-around; }
    
# Imagen 10
