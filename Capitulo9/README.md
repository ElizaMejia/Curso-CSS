# Efectos de bor9de y caja

Agregar efectos de borde como esquinas redondeadas o sombras probablemente ha sido responsable de más elementos de marcado vacíos extraños que casi 
cualquier otra cosa en el mundo del desarrollo web. Cosas que deberían haber sido simples a menudo implicaron soluciones increíblemente complejas.
La segunda parte de nuestro análisis del módulo Fondos y bordes explora nuevos métodos para decorar elementos sin marcas adicionales. Aprenderá cómo hacer esquinas redondeadas, usar imágenes para los bordes y agregar sombras paralelas.

## Dando a tus fronteras esquinas redondeadas

El módulo Fondos y bordes presenta una forma de redondear las esquinas de sus elementos usando solo CSS. Cada esquina se trata como un cuarto de elipse, que está definida por una curva que se dibuja entre un punto de la X-eje y un punto en el y-eje. 

Un cuarto de elipse puede ser regular, lo que significa que la longitud a lo largo de ambos ejes es la misma, o irregular, lo que significa que la longitud a lo largo de cada eje es diferente. 

![Imagen 1 ilustrando el capitulo 9](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo9/Imagenes/C9/Imagen1_C9.png)


CSS3 define estas curvas usando elradio-frontera propiedad. Con esta propiedad, puede definir el radio del cuarto de elipse de forma sencilla, utilizando la siguiente sintaxis:

     E { border-v-h-radius: x y; }

En esta sintaxis,ves un valor de palabra clave de arriba o abajo; h es un valor de palabra clave de izquierda o bien; y el X y Y los valores son longitudes a lo largo de los ejes que definen la curva del cuarto de elipse. 

     div { border-top-right-radius: 20px 20px; }

Esta sintaxis redondeará la esquina superior derecha de un div elemento con un radio de 20px horizontal y verticalmente, que es una curva regular.
De hecho, para curvas regulares,radio-fronterale permite simplificar aún más al omitir el X o el Y valor; si no se especifica un valor, se supone que ambos son iguales. Entonces, si deseas aplicar ese radio a cada esquina de tu elemento, usa este código:

     div {
            border-top-left-radius: 20px;
            border-top-right-radius: 20px;
            border-bottom-right-radius: 20px;
            border-bottom-left-radius: 20px;
         }

Para crear una forma con esquinas redondeadas irregulares, simplemente use diferentes valores en las propiedades individuales:
  
     div {
              border-top-left-radius: 10px 20px;
              border-top-right-radius: 10px 20px;
              border-bottom-right-radius: 10px 20px;
              border-bottom-left-radius: 10px 20px;
         }
 
Puede comparar los dos ejemplos de código diferentes en la Figura inferior: la forma de la izquierda usa el primer fragmento y tiene cuatro esquinas curvas regulares, y la de la derecha es el resultado del segundo fragmento con cuatro esquinas irregulares (iguales).


![Imagen 2 ilustrando el capitulo 9](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo9/Imagenes/C9/Imagen2_C9.png)

## La taquigrafía del radio fronterizo

Si tener que escribir una propiedad diferente para cada esquina le parece bastante repetitivo, le alegrará saber que hay una propiedad abreviada disponible. Al igual que conancho de borde, margen,y relleno,puede especificar uno, dos, tres o cuatro valores. Sin embargo, cuando esos valores se refieren a lados, el radio-frontera los valores se refieren a las esquinas, comenzando en la parte superior izquierda:

     E { border-radius: [top-left] [top-right] [bottom-right] [bottom-left]; } 
     E { border-radius: [top-left] [top-right & bottom-left] [bottom-right]; } 
     E { border-radius: [top-left & bottom-right] [top-right & bottom-left]; } 
     E { border-radius: [top-left & top-right & bottom-right & bottom-left]; }

Entonces, si quiero aplicar un valor de 20px a las esquinas superior izquierda y superior derecha de un divi,y 10px en las esquinas inferior derecha e inferior izquierda, aquí está el código que se usa:

     div { border-radius: 20px 20px 10px 10px; }

Resultados del "Ejemplo 1", del documento Ejemplos_Capitulo9.css subido en el presente repositorio:

1. El primer cuadro tiene dos valores para radio- frontera:Las esquinas superior izquierda e inferior derecha tienen un valor de 0, por lo que son cuadradas, pero las esquinas superior derecha e inferior izquierda están redondeadas con un radio de 20 px. 
2. El segundo cuadro tiene tres valores: la esquina superior izquierda vuelve a ser cuadrada, pero ahora las esquinas superior derecha e inferior izquierda tienen un radio de 10 px, y la esquina inferior derecha tiene un valor de 20 px.
3. El tercer cuadro tiene cuatro valores: las esquinas superior izquierda y superior derecha tienen un valor de 0, por lo que están cuadradas, mientras que las esquinas inferior derecha e inferior izquierda tienen radios de 20 px.

![Imagen 3 ilustrando el capitulo 9](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo9/Imagenes/C9/Imagen3_C9.png)


También puedes utilizar la sintaxis taquigráfica con curvas irregulares. Para lograr este efecto, enumera los valores separados por una barra (/): 

     radio-borde: {radio horizontal/radio vertical; }

Cada lado de la barra puede contener entre uno y cuatro valores, como ocurre con la abreviatura de curvas regulares. Esto significa, por ejemplo, que podría tener un valor para el radio horizontal y cuatro valores separados para los radios verticales.

Resultados del "Ejemplo 1.1", del documento Ejemplos_Capitulo9.css subido en el presente repositorio:

1. El primer cuadro tiene cuatro esquinas iguales de 20 px horizontales y un radio vertical de 10 px. 
2. El segundo cuadro tiene dos esquinas de 20px/10px y dos de 20px/20px. 
3. El tercer cuadro tiene una esquina superior izquierda de 10 px/20 px, una esquina superior derecha y una esquina inferior izquierda de 20 px/ 10 px, y una esquina inferior derecha de 20 px/20 px.

![Imagen 4 ilustrando el capitulo 9](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo9/Imagenes/C9/Imagen4_C9.png)


## Usar valores porcentuales

Los ejemplos hasta ahora en este capítulo utilizan unidades de longitud, pero también puedes definir radio-frontera usando un valor porcentual, que es el porcentaje de la longitud del lado del elemento al que se aplica. Esto te resultará especialmente útil si quieres crear un círculo perfecto en CSS: un elemento cuadrado con cuatro curvas iguales de la mitad de cada lado crea un elemento perfectamente redondo.

Resultados del "Ejemplo 2", del documento Ejemplos_Capitulo9.css subido en el presente repositorio:

1. El elemento de la izquierda tiene la longitud más ancha, por lo que el redondeo de las esquinas crea una elipse.
2. A la derecha, el elemento tiene igual altura y anchura, lo que da como resultado una esfera perfecta.

![Imagen 5 ilustrando el capitulo 9](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo9/Imagenes/C9/Imagen5_C9.png)


# usando imágenes para bordes

Otra forma común de diseñar elementos es utilizar imágenes de fondo como bordes decorativos. Con CSS2, sin embargo, no había forma de lograr esto y tenía que usar mucho marcado adicional para obtener el efecto deseado, con la consiguiente penalización en la semántica y la mantenibilidad. CSS3 introduce una serie de propiedades que proporcionan una sintaxis sencilla para aplicar bordes decorativos.

## fuente-imagen-borde

La primera propiedad,fuente-imagen-borde,establece la fuente de la imagen que se utilizará para el borde. Toma un valor único, que es un tipo de datos de imagen; para la mayoría de los navegadores eso es solo el URL() función. 

     E { border-image-source: url('foo.png'); }

## corte-imagen-borde

Una vez que tenga la fuente de la imagen para el borde, deberá cortarla. La propiedad corte- imagen-borde acepta entre uno y cuatro valores, cada uno de los cuales se asigna a un lado de un elemento, similar a margen, relleno, radio fronterizo,etcétera. Estos valores se utilizan para establecer una distancia desde cada borde de la imagen, marcando el área utilizada para “enmarcar” el elemento.

Eche un vistazo a este código:

     E { border-image-slice: 34; }

Tenga en cuenta aquí que no se utilizan unidades en el valor numérico. El número tiene dos propósitos: para imágenes de mapa de bits (como JPG o PNG), las unidades son valores de píxeles; pero para imágenes vectoriales (como SVG), son valores de coordenadas. También puede utilizar valores porcentuales como alternativa.
En mi código de ejemplo, proporcioné solo un valor único, que establece el área que quiero dividir: 34 píxeles desde arriba, derecha, abajo e izquierda. 
La imagen inferior muestra cómo se utiliza este valor para dividir la imagen de origen en nueve segmentos: cuatro esquinas (c1, c2, etc.), cuatro lados (conocidos como rebanadas—slice1, slice2, etc.) y el relleno central. Cada uno de estos sectores se colocará en el borde de un elemento de destino en posiciones equivalentes.

![Imagen 6 ilustrando el capitulo 9](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo9/Imagenes/C9/Imagen6_C9.png)

Resultados del "Ejemplo 3", del documento Ejemplos_Capitulo9.css subido en el presente repositorio:

Los sectores de la imagen superior e inferior tienen la misma altura que los bordes superior e inferior, por lo que la imagen se aplica a su altura natural, mientras que los sectores izquierdo y derecho se aplican a bordes que tienen menos de la mitad de su ancho, por lo que la imagen se aplasta para ajustarse. Los cortes de las esquinas están distorsionados para adaptarse a las dos dimensiones diferentes.

![Imagen 7 ilustrando el capitulo 9](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo9/Imagenes/C9/Imagen7_C9.png)

El comportamiento predeterminado de las imágenes de borde es usar solo los cortes y esquinas del borde, dejando el centro del elemento en blanco para que se muestren sus propias propiedades de fondo. La propiedad corte-imagen-borde tiene un valor de palabra clave opcional de llenar,sin embargo; Si en llenar se incluye la palabra clave Si, el área de la imagen dentro de los cortes se aplicará sobre el fondo del elemento en el lugar apropiado.

     E { border-image-slice: value fill; }

## ancho-de-imagen-del-borde

Por ejemplo, si el elemento tiene un borde de 10 píxeles de ancho pero sus sectores tienen 40 píxeles de ancho, cada sector se condensará a un cuarto de su alto o ancho para que quepa. Puedes controlar esto usando el ancho-de-imagen- de la propiedad -borde:

     E { border-image-width: value; }

Como ancho del borde o corte de imagen de borde,el valor en realidad, aquí puede haber hasta cuatro valores, para que coincidan con los lados del elemento, y cada uno puede ser una longitud, un porcentaje o un número sin unidades.
El valor crea un borde "virtual" en el elemento, con lo que quiero decir que no tiene impacto en el diseño o flujo de la página; a diferencia de ancho del borde,la frontera que valor crea es sólo visual y no tiene ningún efecto en el modelo de caja. 

Resultados del "Ejemplo 4", del documento Ejemplos_Capitulo9.css subido en el presente repositorio:

El elemento de la izquierda tiene un borde de 34 px en cada lado y no tiene ningún borde explícito .ancho-de-imagen-del-borde valor, por lo que el contenido del texto comienza dentro del borde como era de esperar; el elemento de la derecha, sin embargo, tiene solo un borde de 1px pero un ancho-de-imagen-del-borde valor de 34px. Aunque los sectores de la imagen se aplican de la misma manera, el contenido del texto se ubica sobre la parte superior del borde "virtual" en el elemento de la derecha.

![Imagen 8 ilustrando el capitulo 9](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo9/Imagenes/C9/Imagen8_C9.png)

## inicio-imagen-borde

De forma predeterminada, una imagen de borde comienza a mostrarse desde el exterior del cuadro de borde, moviéndose hacia el cuadro de contenido; pero puede cambiar este comportamiento predeterminado haciendo que la imagen comience desde fuera del cuadro de borde. Esto lo haces con el inicio-imagen-borde propiedad, que toma (los ya habituales) cuatro posibles valores de longitud, uno para cada lado. Por ejemplo, para comenzar la imagen del borde en 10 píxeles desde arriba y desde abajo y 5 píxeles desde la izquierda y la derecha, use esta regla:

     E { border-image-outset: 15px 30px; }

## repetición-imagen-borde

Una propiedad más está relacionada con las imágenes de bordes:repetición-imagen-borde. Esta propiedad controla cómo la imagen se ajusta a la longitud de cada lado entre las esquinas:

     E { border-image-repeat: keyword; }

1. Estirar donde la porción de la imagen se estira para llenar la longitud del borde.
2. Repetir aplica el corte en su longitud natural, repitiéndolo hasta que llena la longitud del borde al que se aplica, por lo que la rebanada podría cortarse si no encajaba en la longitud un número entero de veces.
3. Redondo, se comporta como repetir excepto que escala el corte hacia arriba o hacia abajo para que se ajuste mejor a la longitud del borde, sin cortarlo.
   
Estos tres elementos(imagen inferior) tienen los mismos valores aplicados a todos los imagen-borde propiedades, excepto repetición-imagen-borde. Para esta propiedad, el primer elemento tiene el valor predeterminado,estirar; el segundo, repetir;y el elemento final,redondo.

![Imagen 9 ilustrando el capitulo 9](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo9/Imagenes/C9/Imagen8_C9.png)

Se puede utilizar dos de los tres valores de palabras clave en la propiedad; el primero controla la repetición horizontal, el segundo, la vertical. Entonces, si desea estirar su elemento a lo largo de los bordes superior e inferior y redondearlo a la izquierda y a la derecha, use esta regla:

     E { border-image-repeat: stretch round; }

## La propiedad taquigráfica de la imagen del borde

Para ahorrar tiempo y pulsaciones de teclas, puede utilizar el imagen-borde abreviatura de todas las propiedades que acabamos de describir. La sintaxis se ve así:

     E { border-image: source slice / width / outset repeat; }

El siguiente ejemplo de código muestra todas las propiedades individuales aplicadas a un elemento y luego las mismas propiedades aplicadas a otro elemento usando la propiedad abreviada:


     E{
          border-image-source: url('foo.png'); 
          border-image-slice: 25 10 fill; 
          border-image-width: 25px 10px; 
          border-image-outset: 5px; 
          border-image-repeat: round;
       }

     F { border-image: url('foo.png') 25 10 fill / 25px 10px / 5px round; }


## Soporte del navegador

Toda las propiedades imagen-borde de esta sección son compatibles con Chrome, Firefox, Safari 6+ e Internet Explorer 11+. Algunos navegadores más antiguos, en particular Safari móvil 5.1 y versiones anteriores, y el navegador estándar en Android 4.3 y versiones anteriores, admiten imágenes de bordes, pero solo usan el imagen-bordecorto-mano y, aun así, sin la ancho-de-imagen-del-borde y inicio-imagen-borde propiedades.

# Soltar sombras

En el Capítulo 6, analizamos una forma de agregar sombras paralelas al texto con la sombra de texto propiedad, pero CSS3 también tiene un método para agregar sombras a los elementos del cuadro se usa la propiedad sombra de la caja; la sintaxis es similar a la desombra de texto:

     E { box-shadow: inset horizontal vertical blur-radius spread color; }
        
El primer valor,recuadro,es una palabra clave opcional que establece si la sombra se encuentra dentro o fuera del elemento. 
Los siguientes dos valores son, al igual que con sombra de texto,longitudes que fijan el horizontal y vertical distancia de la sombra a la caja; Si quieres tener una sombra, estos valores son obligatorios.

El siguiente valor establece el radio de desenfoque y es otro valor de longitud y, nuevamente, funciona exactamente como en sombra de texto.Entonces tienedes otro valor de longitud más, que establece la distancia que se extiende la sombra. Una longitud positiva hace que la sombra sea más grande que su elemento y una longitud negativa la hace más pequeña. Ambos radio de desenfoque y desparramar son opcionales.
Finalmente tienes el color valor, también opcional, que, si no se especifica, toma por defecto el color heredado (normalmente negro).

Resultados del "Ejemplo 5", del documento Ejemplos_Capitulo9.css subido en el presente repositorio:

1. La primera es la sombra más simple, simplemente distanciada 4px tanto horizontal como verticalmente del elemento, usando el color heredado. ç
El segundo tiene los mismos valores de distancia que el primero pero también agrega un radio de desenfoque de 3px para suavizar los bordes de la sombra. 
2. El tercero tiene una distancia de 12 px a lo largo de ambos ejes pero un valor de extensión negativo (−6 px), lo que hace que la sombra sea más pequeña que su cuadro. 
3. El cuarto ejemplo tiene una sombra de color gris medio con una distancia vertical negativa, lo que significa que la sombra cae sobre el elemento en lugar de debajo de él.
4. El quinto cuadro tiene dos sombras aplicadas, con cada conjunto de valores separados por una coma. El primer valor establecido es el mismo que en el cuarto cuadro, y el segundo crea una sombra negra (o color heredado) con una distancia horizontal negativa, lo que hace que la sombra caiga a la izquierda del cuadro.

![Imagen 10 ilustrando el capitulo 9](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo9/Imagenes/C9/Imagen10_C9.png)

# Insertar sombras

Mencioné brevemente el opcional .recuadro palabra clave al comienzo de la sección anterior. Si está presente, esta palabra clave dibuja una sombra en el interior del cuadro, pero también tiene el efecto de "voltear" la sombra hacia el otro lado del cuadro. Lo que quiero decir es que donde un regular, es decir,comienzo—sombra con positivo X y Y los valores aparecerían en la parte inferior derecha del cuadro, una sombra insertada aparecería en la parte superior izquierda.

Resultados del "Ejemplo 5", del documento Ejemplos_Capitulo9.css subido en el presente repositorio, pero ahora utilizando esta propiedad; Todos los valores de desplazamiento, radio de desenfoque y color son los mismos, pero las sombras ahora aparecen en el interior de los cuadros y en las esquinas opuestas.

![Imagen 11 ilustrando el capitulo 9](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo9/Imagenes/C9/Imagen11_C9.png)



