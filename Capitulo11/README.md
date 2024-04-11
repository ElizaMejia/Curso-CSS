# Radiantes G

A degradado en este contexto está la transición gradual entre dos o más colores: un estándar de diseño durante muchos años y que uno podría pensar que
sería bastante sencillo de traducir a CSS, pero que tiene una larga y tortuosa historia en la Web.
Los gradientes CSS se introdujeron por primera vez en WebKit en 2008 y llegaron a Safari 4. Sin embargo, la sintaxis que utilizaron era completamente diferente de la que verá en el resto de este capítulo y otros proveedores de navegadores la consideraron demasiado compleja. Se presentaron (e incluso implementaron) varias otras propuestas a lo largo de los años siguientes, hasta que se acordó una sintaxis final a finales de 2011. Esta sintaxis final fue adoptada rápidamente por todos los navegadores, y es la que cubriré en este capítulo.


## Gradientes lineales

Un Gradiente lineal es aquel que cambia gradualmente entre colores a lo largo de una línea recta que conecta dos puntos. En su forma más simple, un degradado lineal cambia proporcionalmente entre dos colores a lo largo de toda la línea.
Comenzaré mostrando la sintaxis más corta posible para un gradiente lineal, que se define usando el gradiente lineal() función de valor en el
imagen de fondo propiedad:

     E { background-image: linear-gradient(black, white); }

Cada color por el que desea que pase el degradado se conoce como color topy se pasa a la función en una lista de argumentos separados por comas. Como puedes ver aquí, los degradados requieren al menos dos paradas de color: un inicio y un final. En este ejemplo, el degradado comienza en negro y termina en blanco, pasando gradualmente por todos los tonos intermedios entre los dos valores, ver imagen inferior.

![Imagen 1 ilustrando el capitulo 11](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo11/Imagenes/C11/Imagen1_C11.png)

### Configuración de la dirección del degradado

El eje entre la primera y la última parada de color se conoce como línea de gradiente. En el ejemplo anterior, la línea de degradado comienza en la parte superior del cuadro y se mueve hacia la parte inferior, verticalmente. Esta es la dirección predeterminada. Para establecer una línea de degradado diferente, especifique un lado o esquina objetivo del cuadro pasando un nuevo argumento a la función antes de la lista de paradas de color. El argumento es una cadena de palabras clave, que comienza con ay seguido de una o dos palabras clave de dirección. Por ejemplo, para definir un degradado de negro a blanco que vaya de abajo hacia arriba, utilice este valor:

     E { background-image: linear-gradient(to top, black, white); }

Para cambiar el mismo degradado para que se extienda en diagonal desde la esquina superior izquierda a la inferior derecha, utilice dos palabras clave direccionales:

     E { background-image: linear-gradient(to right bottom, black, white); }

Para un control más preciso sobre la dirección de la línea de degradado, puede utilizar un argumento de ángulo en lugar de las palabras clave direccionales. Los ángulos se pueden declarar usando varias unidades.

El valor del ángulo establece el ángulo de la línea de gradiente:0 grados (o360 grados)va de abajo hacia arriba,45 grados desde abajo a la izquierda hasta arriba a la derecha,90 gradosde izquierda a derecha, y así sucesivamente. Los valores negativos hacen que el gradiente vaya en sentido antihorario.

Por ejemplo, para crear el mismo degradado de arriba a la izquierda a abajo a la derecha como en el ejemplo de código anterior, pero usando un valor de ángulo, usaría este código:

     E { background-image: linear-gradient(135deg, black, white); }

Resultados del "Ejemplo 1", del documento Ejemplos_Capitulo11.css subido en el presente repositorio:

1. El primero de derecha a izquierda
2. El segundo de abajo izquierda a arriba derecha
3. El último un ángulo de 120 grados (aproximadamente, pero no del todo, de arriba a izquierda a abajo) bien).


![Imagen 2 ilustrando el capitulo 11](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo11/Imagenes/C11/Imagen2_C11.png)

### Agregar valores adicionales de parada de color

Hasta ahora he usado un degradado simple con solo dos paradas de color, pero puedes usar más.Cada color que agregue se declara simplemente agregando una nueva parada de color en la lista separada por comas, como en este ejemplo donde Agrego un tercer color negro:

     E { background-image: linear-gradient(black, white, black); }

Las paradas de color se procesan en el orden indicado, por lo que este ejemplo crea un degradado que va del negro al blanco y luego vuelve al negro, imagen inferior.

![Imagen 3 ilustrando el capitulo 11](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo11/Imagenes/C11/Imagen3_C11.png)

Las paradas de color se distribuyen uniformemente a lo largo del degradado, por lo que, en este caso, la parada de color blanco está exactamente a medio camino entre los dos negros, en el punto medio del degradado. Puede modificar esta distribución agregando un valor de longitud o porcentaje después de cada parada de color para cambiar el punto. 

A lo largo de la línea de degradado donde se coloca una parada de color. Por ejemplo, este código coloca el color blanco en el 75 por ciento de la longitud de la línea de degradado:

     E { background-image: linear-gradient(black, white 75%, black); }

![Imagen 4 ilustrando el capitulo 11](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo11/Imagenes/C11/Imagen4_C11.png)

Resultados del "Ejemplo 2", del documento Ejemplos_Capitulo11.css subido en el presente repositorio:

1. El argumento final de color tiene una posición del 75 por ciento, por lo que el color comienza ahí y continúa como un color sólido hasta el final. 
2. La primera parada de color tiene el valor de posición, por lo que se muestra un bloque sólido del color heredado (negro) hasta la marca del 50 por ciento de la línea de degradado, en cuyo punto el degradado comienza a pasar a la parada de color final. valor.
3. Finalmente, tiene tres paradas de color. El segundo comienza en el 50 por ciento, por lo que el primer y segundo color detiene la transición hasta ese punto. La parada de color final se coloca sólo un píxel más allá a lo largo de la línea de degradado, por lo que hay un cambio repentino a ese color (sin transición) y el color continúa hasta el final.

![Imagen 5 ilustrando el capitulo 11](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo11/Imagenes/C11/Imagen5_C11.png)

### Repetición de degradados lineales

En lugar de crear un solo degradado de un lado de un elemento a otro, puede repetir el mismo degradado hasta que el elemento se llene usando e lgradiente- lineal-repetitivo() función. Esta función acepta el mismo conjunto fundamental de valores que gradiente lineal excepto que se requiere un valor de longitud o porcentaje para la parada de color final. He aquí un ejemplo:

     E { background-image: repeating-linear-gradient(white, black 25%); }

Este valor final de parada de color establece el punto en el que el degradado debe terminar y luego comenzar a repetirse. Este código crea un degradado superior-inferior (el predeterminado) entre blanco y negro que cubre el 25 por ciento de la altura del cuadro, lo que significa que se repite cuatro veces, como se muestra en la imagen inferior.

![Imagen 6 ilustrando el capitulo 11](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo11/Imagenes/C11/Imagen6_C11.png)

Resultados del "Ejemplo 3", del documento Ejemplos_Capitulo11.css subido en el presente repositorio:

1. El primer ejemplo utiliza tres paradas de color y establece la dirección para que el degradado vaya de derecha a izquierda. El degradado cubre el 25 por ciento del elemento, por lo que el patrón negro-blanco-negro se repite cuatro veces.
3. El segundo ejemplo utiliza un valor de ángulo de 45 grados entonces el degradado es diagonal y usa unidades de píxeles para las paradas de color. Nuevamente, los degradados son negro- blanco-negro, pero están distribuidos de manera desigual, por lo que el blanco negro cubre 2 píxeles, mientras que el blanco-negro cubre 8 píxeles.
4. El último ejemplo utiliza cuatro paradas de color: negro-negro sobre 2px y luego blanco-blanco sobre 2px. Los valores de longitud bajos impiden un cambio gradual entre los dos colores, creando las líneas diagonales duras que ves aquí.

![Imagen 7 ilustrando el capitulo 11](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo11/Imagenes/C11/Imagen7_C11.png)

## Gradientes radiales

Agradiente radial Es una transición gradual entre colores que se mueve desde un punto central en todas direcciones. En su forma más simple, un degradado radial cambia gradualmente entre dos colores en forma circular o elíptica. Los gradientes radiales se definen con el gradiente radial()función de valor y, al igual que con los degradados lineales, la forma más sencilla de crear uno es pasar dos valores de color como argumentos:

     E { background-image: radial-gradient(white, black); }

![Imagen 8 ilustrando el capitulo 11](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo11/Imagenes/C11/Imagen8_C11.png)

### Usando gradientes radiales

Puede establecer la forma de un degradado radial agregando una palabra clave antes de las paradas de color. El valor predeterminado es elipse,pero puedes usar la alternativa círculo como esto:

     E { background-image: radial-gradient(circle, white, black); }

![Imagen 9 ilustrando el capitulo 11](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo11/Imagenes/C11/Imagen9_C11.png)

El centro predeterminado de un degradado radial (desde el cual irradia el degradado) está en el centro del elemento al que se aplica. Puede cambiar este punto agregando un argumento de posición al gradiente radial()función. Los valores utilizados para establecer esta posición son exactamente los mismos que los utilizados en posición de fondo es decir, una longitud, un porcentaje o palabras clave. Agrega la posición después de la palabra
clave de forma (círculo,en el ejemplo que se muestra aquí), precedido por la palabraen.La posición se establece en el centro-derecha del elemento:

     E { background-image: radial-gradient(circle at 100% 50%, white, black); }

También puedes configurar el medida de un degradado, es decir, el punto donde termina el degradado, utilizando un valor de longitud o posición o una de las cuatro palabras clave de extensión. El argumento de extensión se coloca inmediatamente después de la palabra clave de forma. Por ejemplo, este código crea un degradado circular, cuya extensión es de 50 px, lo que significa que termina a 50 px desde el punto central:

     E { background-image: radial-gradient(circle 50px, black, white); }

Las cuatro posibles palabras clave que puede utilizar al establecer la extensión son esquina más cercana, lado más cercano, esquina más alejada (el valor predeterminado), y lado más lejano.

Resultados del "Ejemplo 4", del documento Ejemplos_Capitulo11.css subido en el presente repositorio:

![Imagen 10 ilustrando el capitulo 11](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo11/Imagenes/C11/Imagen10_C11.png)

### Uso de múltiples valores de parada de color

Al igual que con sus contrapartes lineales, los degradados radiales pueden aceptar múltiples valores de parada de color y valores de longitud o porcentaje para el control de posicionamiento. Cualquier calificador de este tipo se ingresa en una lista separada por comas. 


1. Creado un degradado con tres paradas de color (negroblanco-negro) que irradia desde el centro del cuadro hasta su lado más alejado.
2. Es similar, excepto que la parada de color comienza en el 25 por ciento a lo largo del radio.
3. el degradado comienza en el lado izquierdo del cuadro y termina en el lado derecho, con el color finalizando en el 25 y el 75 por ciento de la longitud. 

![Imagen 11 ilustrando el capitulo 11](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo11/Imagenes/C11/Imagen11_C11.png)


### Repetición de gradientes radiales

Así como el gradiente lineal() la función tiene gradiente-lineal-repetitivo(),a gradiente-radial-repetitivo() se puede utilizar para repetir los argumentos proporcionados hasta que se alcance el límite especificado en la parada de color final. Por ejemplo, el siguiente código crea un degradado circular que se repite blanco y negro cada 20 por ciento hasta alcanzar su extensión. 

     E { background-image: repeating-radial-gradient(circle, black, white 20%); }

![Imagen 12 ilustrando el capitulo 11](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo11/Imagenes/C11/Imagen12_C11.png)

Resultados del "Ejemplo 5", del documento Ejemplos_Capitulo11.css subido en el presente repositorio:

1. Irradia desde la esquina superior derecha y pasa a través de tres paradas de color en más del 15 por ciento del ancho del cuadro, con el límite establecido por el esquina más alejada palabra clave.
2. Se configuro el centro del degradado en el lado izquierdo del cuadro y el límite en la esquina más alejada, usando un degradado blanco- blanco (sólido) para 10 px y luego un degradado blanco-negro para 5 px.
3. Un degradado blanco, negro y blanco se repite en un radio muy pequeño de 2 píxeles, creando el patrón de interferencia.

![Imagen 13 ilustrando el capitulo 11](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo11/Imagenes/C11/Imagen13_C11.png)

## Múltiples gradientes

Debido a que los gradientes se aplican con el imagen de fondo propiedad, puede usar la sintaxis de múltiples valores de fondo de CSS3, para aplicar múltiples gradientes a un elemento usando valores separados por comas. 

Resultados del "Ejemplo 6", del documento Ejemplos_Capitulo11.css subido en el presente repositorio:

1. El ejemplo de la izquierda muestra dos degradados lineales aplicados a un elemento: de arriba a la izquierda a abajo a la derecha y de arriba a la derecha a abajo a la izquierda. La parada de color final tiene un valor de transparente para permitir que el segundo degradado se vea debajo de él.
2. El ejemplo de la derecha muestra tres degradados radiales, cada uno de los cuales se extiende hasta el lado más cercano, con el centro de cada uno en un punto diferente. Como en el primer ejemplo, la última parada de color tiene un valor de transparente para permitir que las capas de abajo se vean.

![Imagen 14 ilustrando el capitulo 11](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo11/Imagenes/C11/Imagen14_C11.png)
