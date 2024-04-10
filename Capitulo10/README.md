# Color y Opacidad

El módulo de color CSS 3 introduce los conceptos de opacidad a través de la propiedad opacidad y el canal Alfa de color. Además, el módulo de color CSS agrega un modelo de color completamente nuevo, que es más intuitivo y más fácil de modificar para encontrar el tono perfecto.
El módulo de color es una recomendación del W3C y está bien implementado en IE9 y superiores y en todos los demás navegadores importantes. 

## La propiedad de opacidad

La opacidad es, estrictamente hablando, la medida de la resistencia de un objeto a la luz: cuanto más opaco es algo, menos luz deja pasar. Un objeto sin opacidad es completamente transparente.
En CSS, la opacidad se mide usando la propiedad opacidad. En esencia, con opacidad,usted está configurando qué parte del fondo se puede ver a través del elemento especificado.La propiedad opacidad tiene la siguiente sintaxis:

     E { opacity: number; }

El valor numerico es una fracción decimal, es decir, un número entre 0,0 y 1,0, donde 0,0 es completamente transparente, 1,0 es completamente opaco y cualquier valor entre esos dos es una combinación de opacidad y transparencia. Por ejemplo, para configurar un elemento para que sea 50 por ciento opaco (o 50 por ciento transparente, dependiendo de si el vaso está medio vacío o medio lleno), se utiliza la siguiente regla:

     E { opacity: 0.5; }

Resultados del "Ejemplo 1", del documento Ejemplos_Capitulo19.css subido en el presente repositorio:

1. En el primer ejemplo (izquierda) no tiene un valor establecido explícitamente para opacidad,por lo que el valor predeterminado es 1.0, o completamente opaco: su fondo es blanco. 
2. El siguiente (medio) tiene un valor de 0,66, por lo que su opacidad se reduce en un tercio, lo que hace que el fondo blanco aparezca como gris claro (una mezcla del color de fondo negro del elemento principal y el color de fondo blanco del elemento en sí, que se ve a través). 
3. Finalmente, el último (derecha) tiene un valor de opacidad de 0,33, por lo que puede considerarse dos tercios transparente, lo que hace que la caja tenga un color gris más oscuro.

![Imagen 1 ilustrando el capitulo 10](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo10/Imagenes/C10/Imagen1_C10.png)

Ahora, aquí hay un punto extremadamente importante para recordar acerca de esta propiedad: la opacidad afecta no solo al elemento al que se aplica sino también a todos los elementos secundarios de ese elemento. Si establezco un opacidad valor de 0,5 en un elemento, sus hijos nunca serán más opacos que eso. Esta configuración no puede ser anulada por ninguna otra propiedad; o mejor dicho, nunca puedes hacer que un elemento sea más opaco que su padre, pero sí poder hacerlo menos opaco.
CSS3 tiene un nuevo método para sortear esta limitación; se llama canal Alfa y lo explico en la siguiente sección.

## Valores de color nuevos y ampliados

CSS2.1 permitía tres métodos para especificar valores de color: palabras clave (negro), notación hexadecimal (#000000),y RGB (0,0,0).En CSS3, el rango se amplía mediante un método completamente nuevo para especificar colores, así como la introducción de opacidad a través del canal Alfa.

### El canal alfa

El canal alfa es la medida de la opacidad de un color, a diferencia de la propiedad opacidad, que es la medida de la opacidad de un elemento. Por lo tanto, aunque los elementos secundarios pueden heredar los valores de color que utilizan Alpha como cualquier otro valor de color, la opacidad general del elemento no se ve afectada.
CSS3 introduce Alpha como un valor en el RGBA modelo de colores. RGBA significa Rojo,Verde,Azul,Alfa, y se aplica con el rgba()función. La sintaxis es la misma que para el rgb()valor de función utilizado en CSS2, pero con el valor Alfa especificado por un argumento adicional separado por comas al final:

     E { color: rgba(red, green, blue, alpha); }

El valor del argumento alfa es el mismo que el valor proporcionado para la opacidad: una fracción decimal de 0,0 a 1,0, que es una vez más una medida.

Entre transparencia total (0,0) y opacidad total (1,0). Si desea que un elemento tenga un color de primer plano negro con una opacidad del 50 por ciento, utilice el siguiente código:

     E { color: rgba(0,0,0,0.5); }

Como se mencionó,rgba()difiere del opacidad propiedad de dos maneras: 
1. Primero, rgba()es un valor de color, por lo que no puedes, por ejemplo, usarlo para cambiar la opacidad de una imagen (o un elemento con una imagen de fondo).
2. En segundo lugar, aunque el valor de la función rgba() se puede heredar, los elementos secundarios pueden anularse con un rgba()valor propio.

Resultados del "Ejemplo 2", del documento Ejemplos_Capitulo19.css subido en el presente repositorio:

Ambos cuadros tienen el mismo nivel de transparencia, pero en el primero, el opacidadel valor ha sido heredado por su hijo pag elemento, haciendo también que el texto sea semitransparente. En el segundo cuadro, el valor rgba() se aplica estrictamente a la color de fondo del .texto elemento, por lo que el elemento pagconserva su color negro totalmente opaco.

![Imagen 2 ilustrando el capitulo 10](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo10/Imagenes/C10/Imagen2_C10.png)

Resultados del "Ejemplo 2.1", del documento Ejemplos_Capitulo19.css subido en el presente repositorio:

1. En el primer cuadro,rgbareduce la opacidad desombra de la caja; estableciendo el valor Alfa en 0,7 -permite que se vea parte del fondo, haciendo que la sombra sea más "realista". 
2. El siguiente ejemplo muestra un negro 50 por ciento opaco.
3. En el siguiente ejemplo, el valor Alfa de la propiedad color se ha establecido en 0,6-,lo que hace que el texto parezca semiopaco. 
4. Y finalmente el último ejemplo muestra otro efecto de sombra, esta vez en el sombra de texto propiedad. El valor Alfa se establece en 0,6X,lo que, una vez más, crea una sombra más realista.

![Imagen 3 ilustrando el capitulo 10](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo10/Imagenes/C10/Imagen3_C10.png)

### RGBA y degradación elegante

Los navegadores más antiguos que no admiten valores RGBA (en particular, IE8) ignorarán cualquier regla que los utilice y utilizarán de forma predeterminada un valor heredado o especificado previamente. Para compensar, debe especificar el color dos veces (primero sin y luego con un valor Alfa) usando la cascada para garantizar que se implemente el color correcto:

     pag {
           color: #F00;
           color: rgba(255,0,0,0.75);
         }

En este ejemplo, los navegadores que no admiten valores RGBA ignoran el segundocolor propiedad y aplicar la primeracolorpropiedad. Por supuesto, este resultado significa que se utilizará un color completamente opaco en lugar de uno semiopaco, así que revise su diseño minuciosamente para asegurarse de que no se vea afectado negativamente.

### Tono, saturación, luminosidad

HSL-Lo que significa: Matiz,Saturación,Ligereza(aveces llamado Luminancia)—es una representación de coordenadas cilíndricas del espacio de color, ver la imagen inferior.

![Imagen 4 ilustrando el capitulo 10](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo10/Imagenes/C10/Imagen4_C10.png)

Todos los colores posibles están dispuestos en un cilindro con un eje central. El ángulo alrededor del eje es el matiz; la distancia desde el eje es la saturación; y la distancia a lo largo del eje es la ligereza. La combinación de esos tres valores crea un color único.

1. Matiz representa los colores principales, comenzando y terminando con rojo (0 o 360) e incluyendo todos los colores principales entre ellos. Piensa en los colores del espectro visible (o los colores del arco iris) que aprendiste en la escuela (rojo, naranja, amarillo, verde, azul, índigo y violeta) dispuestos alrededor de la circunferencia de un círculo; el valor del tono es un grado alrededor de esa circunferencia que apunta a un color específico.

2. Saturaciónes la fuerza o intensidad de ese color: 0 por ciento es intensidad cero, lo que hace que el color sea un tono gris, y 100 por ciento es fuerza total, la versión más intensa de ese color.

3. Ligereza es el brillo u oscuridad del color: 50 por ciento es el color verdadero, 0 por ciento es negro y 100 por ciento es blanco.
   
HSL se aplica con el hsl()Función de valor de color. Se necesitan tres argumentos, con una sintaxis similar argb():

     E { color: hsl(hue,saturation,lightness); }

El valor matiz es un número entre 0 y 360 (los grados alrededor de la rueda de tono), y saturación y ligereza aceptar valores de 0 por ciento a 100 por ciento, observar los ejemplos de la tabla inferior.

![Imagen 5 ilustrando el capitulo 10](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo10/Imagenes/C10/Imagen5_C10.png)

La ventaja de HSL sobre RGB (o hexadecimal) es que permite probar diferentes variantes de un color más rápidamente, como hacer que un determinado color sea más claro/oscuro o más/menos intenso. La flexibilidad de HSL lo hace más útil para los diseñadores web. 

### HSLA

Si ha decidido que HSL es el método de color para usted, también podrá utilizar el canal Alfa para transparencia con el hsla() Función de valor de color. Como su contraparte rgba(), hsla() simplemente extiende la combinación de colores con un argumento adicional en la función:

     E { color: hsl(hue,saturation,lightness,alpha); }

Entonces, por ejemplo, si quieres un elemento con un color valor de rojo y 50 por ciento de opacidad, se utiliza esta regla:

     E { color: hsl(0,100%,50%,0.5); }

### La variable de color: color actual

Además de los nuevos métodos de color que acabo de describir, CSS3 también introduce un nuevo color palabra clave de valor:color actual.Esta palabra clave actúa como una variable para el color actual: el valor de color actual porque un elemento es el valor de su propio color propiedad. 

Resultados del "Ejemplo 3", del documento Ejemplos_Capitulo19.css subido en el presente repositorio:

Uno h2 se muestra en negro (negro)texto en el valor predeterminado ( blanco) fondo, y el otro en blanco texto en un negro fondo. A continuación, uso el color actual palabra clave como valor para el borde inferior propiedad en el abbr elementos. 

Porque el primero h2 tiene un color valor de negro,el color de la borde inferior propiedad de la abbr elemento también es negro.porque el segundo h2 tiene un color valor de blanco,el borde inferior propiedad de la abbr el elemento tiene el mismo color. Estos valores han asumido el color propiedad de sus elementos padres.

El color actual palabra clave significa que no tengo que especificar el color del borde para cada instancia del abbr elemento.

![Imagen 6 ilustrando el capitulo 10](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo10/Imagenes/C10/Imagen6_C10.png)
