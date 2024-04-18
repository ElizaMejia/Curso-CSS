# Transiciones y Animaciones

Estos módulos permiten la animación de propiedades de elementos, agregando movimiento a páginas que de otro modo serían estáticas, incluso cuando JavaScript no está disponible.

La diferencia entre transiciones y animaciones es que las primeras son implícito y estos últimos son declarado. Eso significa que las transiciones solo tienen efecto cuando la propiedad a la que se aplican cambia de valor, mientras que las animaciones se ejecutan explícitamente cuando se aplican a un elemento.

# Transiciones

En CSS, un transiciónes una animación que mueve una propiedad entre dos estados.
Las transiciones son una implícito animación, lo que significa que se activan solo cuando se establece un nuevo valor para una propiedad CSS; esto podría ocurrir cuando se aplican nuevos valores al pasar el mouse o mediante manipulación de JavaScript. Para que se produzca una transición, deben darse cuatro condiciones: un valor inicial, un valor final, la transición en sí y un desencadenante.
Aquí hay un ejemplo de esas cuatro condiciones en una transición simple:

     div {
            background-color: black;
            transition: background-color 2s;
         }

     div:hover { background-color: silver; }

El div elemento proporciona el valor inicial (color de fondo: negro)y la transición (color de fondo 2s).El desencadenante es el:flotar pseudo clase, que establece el valor final (plata)Para el color de fondo propiedad.
Así que aquí tenemos un div elemento con fondo negro que, al pasar el ratón sobre él, pasa suavemente a plateado. Todas las transiciones actúan a la inversa cuando el disparador ya no está activo, por lo que cuando se mueve el mouse fuera del div,el fondo vuelve suavemente a negro.

## Propiedad de transición

La primera propiedad nueva,propiedad de transición,especifica qué propiedad (o propiedades) de un elemento se animarán. Aquí está la sintaxis:

     E { transition-property: keyword; }

Un valor de palabra clave aceptable es todo o ninguno o una propiedad CSS válida. El valor predeterminado es todo,lo que significa que todas las propiedades válidas serán animadas.

He aquí un ejemplo de propiedad de transición:

     h1 {
           font-size: 150%;
           transition-property: font-size;
        }

Este código establece un valor inicial de 150% sobre el tamaño de fuente propiedad y declara que esta es la propiedad a la que se realizará la transición cuando se active el activador (aún no especificado). 

## Duración de la transición

La siguiente propiedad es duración de la transición,que define el tiempo que tarda en completarse la transición. Aquí está la sintaxis:

     E { transition-duration: time; }

El valor tiempo es un número con una unidad de EM(milisegundos) o s(segundos). Como 1000 milisegundos equivalen a 1 segundo, un valor de 1,25s es lo mismo que 1250 ms.El valor predeterminado es 0 (cero), lo que significa que esta propiedad es la única necesaria para crear una transición. Puede ocurrir una transición si usted declara una duración de la transición sin un propiedad de transición (ya que por defecto es todo,entonces todas las propiedades válidas se animarán) pero no al revés.
Para que la transición del ejemplo de la sección anterior se realice durante un período de dos segundos, agregue este código:

     h1 {
           font-size: 150%;
           transition-property: font-size;
           transition-duration: 2s;
        }
Aunque puede proporcionar valores negativos a esta propiedad, se interpretarán como valores predeterminados 0.

## Función de sincronización de transición

Para controlar la manera en que un elemento pasa de un estado a otro, se utiliza el función de sincronización de transición propiedad. Esta propiedad permite variaciones en la velocidad a lo largo de la transición, lo que le da control sobre el ritmo de la animación. Esta propiedad tiene tres tipos de valores diferentes: una palabra clave, el Bézier cúbico() función, o la pasos() función. 

### Palabras clave de función de sincronización

La sintaxis del función de sincronización de transición la propiedad cuando se usa con una palabra clave es bastante sencilla:

     E { transition-timing-function: keyword; }

Los posibles valores de palabras clave son facilidad, lineal, fácil entrada, fácil salida,y
facilidad para entrar y salir.

1. El valor predeterminado es facilidad,que comienza lentamente, acelera rápidamente y vuelve a desacelerarse al final. 
2. El valor lineal progresa de manera constante desde el inicio de la transición hasta el final, sin variación en la velocidad.  
3. Finalmente,facilidad de entrada y salida comienza lentamente, acelera a la mitad y luego vuelve a desacelerarse al final, similar, pero menos dramático, que el facilidad valor.

Una vez explicado esto, agreguemos una función de sincronización simple a la transición de ejemplo:

     h1 {
           font-size: 150%;
           transition-property: font-size; 
           transition-duration: 2s; 
           transition-timing-function: ease-out;
        }

### La curva cúbica de Bézier

Si desea un control más preciso sobre el función de sincronización de transición propiedad, debe utilizar el Bézier cúbico()función. Aquí está la sintaxis:

     E { transition-timing-function: cubic-bezier(x1, y1, x2, y2); }

Una curva de Bézier cúbica es una curva suave y continua que pasa por cuatro puntos trazados en una cuadrícula que va de 0 a 1 a lo largo de ambos ejes. Los cuatro puntos se conocen como PAG0,PAG1,PAG2, y PAG3. Definen la curvatura y se trazan con pares de (X,y) coordenadas, donde la primera (PAG0) siempre está en (0, 0) y el último ( PAG3) siempre está en (1, 1). Los otros dos puntos están definidos en la función: (x1,y1) y (x2,y2). Un ejemplo, el que se muestra en la la imagen inferior.

![Imagen 1 ilustrando el capitulo 14](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo14/Imagenes/C14/Imagen1_C14.png)
![Imagen 2 ilustrando el capitulo 14](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo14/Imagenes/C14/Imagen2_C14.png)

Usarías el siguiente CSS para representar esta curva (recuerda, no necesitas definir PAG0 y PAG3 porque siempre tienen los mismos valores):

     E { transition-timing-function: cubic-bezier(0.6, 0.1, 0.15, 0.7); }

Una animación lineal avanza en línea recta desde (0, 0) a (1, 1), pero esta animación de ejemplo sigue la progresión de la curva hacia el punto final durante la duración establecida. Si imagina que la duración es de 1 segundo, puede ver que la velocidad aumenta gradualmente al principio, entre 0 y (aproximadamente) 0,5 segundos, y luego aumenta bruscamente hasta aproximadamente 0,7 segundos, y luego asume una velocidad más lenta hasta el final del animación.

Toda la función de sincronización de transiciónLas palabras clave descritas anteriormente se generan con curvas de Bézier cúbicas. La imagen inferior muestra una tabla con cada una de las palabras clave y sus valores correspondientes para el Bézier cúbico() función.
    
![Imagen 3 ilustrando el capitulo 14](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo14/Imagenes/C14/Imagen3_C14.png)

### La función pasos()

Una alternativa a las transiciones suaves y relajadas es utilizar el pasos() función, que ejecuta la animación en una serie de intervalos escalonados. La sintaxis de la función se ve así:

     E { transition-timing-function: steps(count, direction); }

El valor contar es un número entero que indica cuántos intervalos debe ejecutar la animación y el valor opcional.direcciónes una de dos palabras clave:comenzar o fin (el valor predeterminado): establece el punto en el que se produce el cambio en cada intervalo. 

Veamos un ejemplo muy sencillo de cómo pasos() obras. Eche un vistazo a la siguiente regla, en la que el pasos() la función tiene un argumento de recuento de pasos de 4 y utiliza la forma simple de la función omitiendo la palabra clave de dirección opcional:

     E { transition-timing-function: steps(4); }

Visualizado en la cuadrícula de función de sincronización utilizada para el Bézier cúbico() función, se vería como la imagen inferior. Entonces, en lugar de una sola línea de transición, los pasos son como ver instantáneas de la animación en acción.

![Imagen 4 ilustrando el capitulo 14](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo14/Imagenes/C14/Imagen4_C14.png)

Cuando una animación se muestra en pasos, utilice el dirección palabra clave para seleccionar cuando ocurre el cambio de cada paso: el valor predeterminado fin palabra clave significa que el cambio ocurre al final del paso (pausar, luego cambiar), y la alternativa comenzar significa que el cambio ocurre al inicio del paso (cambiar, luego pausar).
Este proceso también es más fácil de visualizar en la cuadrícula de funciones de sincronización; En el siguiente código, se muestra el mismo recuento de pasos con diferentes palabras clave de dirección:

     E { transition-timing-function: steps(4, start); } 
     E { transition-timing-function: steps(4, end); }
     
![Imagen 5 ilustrando el capitulo 14](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo14/Imagenes/C14/Imagen5_C14.png)


## Retraso de transición

La propiedad final en el transición-* familia es retraso de transición,que establece el momento en que comienza la transición. Aquí está la sintaxis:

     E { transition-delay: time; }

Al igual que conduración de la transición, el valor tiempo es un número con una unidad de milisegundos(EM) o segundos(s).El valor predeterminado es 0 (cero), lo que significa que la transición ocurre tan pronto como el disparador es. Cualquier otro valor positivo inicia la transición una vez transcurrido el período de tiempo especificado.

Por ejemplo, si desea establecer un retraso de un cuarto de segundo al inicio de la transición de ejemplo, este es el código que usaría:

     h1 {
           font-size: 150%;
           transition-property: font-size; 
           transition-duration: 2s; 
           transition-timing-function: ease-out; 
           transition-delay: 250ms;
        }

También puedes usar valores negativos para retraso de transición,lo cual tiene un efecto interesante: la transición comienza inmediatamente pero avanza por la cantidad del valor negativo. Por ejemplo si se considera una transición con una duración de 4s pero un retraso de -2:

     E {
          transition-duration: 4s; transition-delay: -2s;
       }

Cuando se activa, la transición comienza inmediatamente, pero como si ya hubieran pasado dos segundos (siendo dos segundos la duración menos el retraso). En este caso, la animación comenzaría a mitad de la transición.

## La propiedad taquigráfica de transición

A lo largo de esta sección, he creado un ejemplo de transición propiedad por propiedad. Hasta ahora, el código se ve así:

     h1 {
           transition-property: font-size;
           transition-duration: 2s;
           transition-timing-function: ease-out;
           transition-delay: 250ms;
        }

Este código parece mucho que escribir para cada transición. Pero, como ocurre con todas las demás propiedades CSS que forman parte de una "familia" (fondo-*, borde-*,y así sucesivamente), el transición-*La familia tiene una taquigrafía. Aquí está la sintaxis:

     E { transition: property duration timing-function delay; }

Una cosa importante a tener en cuenta aquí es que hay dos tiempos valores:duración de la transición y retraso de transición,que debe ser declarado en ese orden. Si sólo se declara uno, la sintaxis supone que es duración de la transición,y el retraso de transiciónse establecerá en el valor predeterminado (o heredado).

Si usa los valores de la transición de ejemplo con la propiedad abreviada, aquí está el resultado:

     h1 { transition: font-size 2s ease-out 250ms; }

Resultados del "Ejemplo 1", del documento Ejemplos_Capitulo14.css subido en el presente repositorio:

La ilustración inferior muestra tres etapas de la transición: la etapa inicial previa a la transición (izquierda) con un tamaño de fuente del 150 por ciento; una etapa intermedia de transición (centro), que se encuentra a poco menos de dos segundos de la animación cuando el tamaño de la fuente ha aumentado; y la etapa final posterior a la transición (derecha), donde el tamaño de fuente es del 600 por ciento.

![Imagen 6 ilustrando el capitulo 14](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo14/Imagenes/C14/Imagen6_C14.png)

## Múltiples transiciones

Puede agregar fácilmente varias transiciones a un elemento proporcionando una lista de valores separados por comas para las propiedades individuales o abreviadas. Siendo ese el caso, los dos ejemplos de código siguientes son válidos:

     E {
          transition-property: border-width, height, padding; 
          transition-duration: 4s, 500ms, 4s;
       }
      
     E { transition: border-width 4s, height 500ms, padding 4s; }

Tenga en cuenta que si una propiedad tiene menos valores que las demás, esa lista de valores se repetirá. 

Resultados del "Ejemplo 2", del documento Ejemplos_Capitulo14.css subido en el presente repositorio:

Aquí he usado el transición taquigrafía para aplicar tres transiciones. 

La primera transición cambia la color de fondo de negro a plata en un lineal función de sincronización, y los dos siguientes cambian la izquierda y arriba propiedades con facilidad de entrada y salida funciones de temporización. El color de fondo la transición se produce en cuatro segundos, y los demás, en dos.

La ilustración inferior muestra tres etapas de la transición: 
1. La primera etapa (izquierda) muestra el elemento previo a la transición, con un fondo negro y ubicado en la parte inferior izquierda de su elemento principal
2. La siguiente etapa (centro) es la transición media, cuando el elemento cambia de color y se mueve hacia la parte superior derecha de su padre
3. La etapa final (derecha) muestra el elemento post-transición, con fondo plateado y en su posición final.

![Imagen 7 ilustrando el capitulo 14](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo14/Imagenes/C14/Imagen7_C14.png)

# Animaciones

Las animaciones se apliquen directamente a elementos con una sintaxis que es más flexible y permite un control más granular. Las animaciones y las transiciones tienen mucha sintaxis en común, pero el proceso para crear animaciones es muy diferente: primero, defines las propiedades y los tiempos, y luego agregas los controles de animación a los elementos que serán animados.


## Fotogramas clave

Puedes pensar en las animaciones CSS como una serie de transiciones, encadenadas en una secuencia. El primer paso para crear tus propias animaciones es definir tu fotogramas clave, que son los puntos que marcan el inicio y el final de una transición. La animación más simple tiene dos fotogramas clave (uno al principio y otro al final), mientras que las más complejas tienen varios fotogramas clave en el medio. 

La ilustración inferior muestra cómo aparecería una animación con tres fotogramas clave.

![Imagen 8 ilustrando el capitulo 14](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo14/Imagenes/C14/Imagen8_C14.png)

En CSS, los fotogramas clave se declaran en @fotogramas clave regla, que tiene la siguiente sintaxis:

     @keyframes name {
                        selector { property : value; }
                     }

El primer valor de @fotogramas clave la regla es nombre; este identificador único se utiliza para llamar a la animación, que analizaré más adelante. Puedes usar prácticamente cualquier valor aquí (usa separación por guiones, no espacios, si quieres un nombre con varias palabras), aunque te sugiero usar una palabra o término que sea relevante para la animación que describe; tus hojas de estilo serán mucho más fáciles de usar. 

El siguiente valor,selector, establece la posición a lo largo de la animación en la que se producirá el fotograma clave. El valor habitual aquí es un valor porcentual; por ejemplo, si desea que el fotograma clave aparezca a mitad de la animación, utilice 50%. También puede utilizar una de las palabras clave,from o to,que son análogos a 0 por ciento y 100 por ciento, respectivamente.

Dentro de cada selector de fotogramas clave hay una declaración CSS o una serie de declaraciones que se aplican a un elemento seleccionado en la etapa especificada de la animación. 
El siguiente código describe una animación simple, a la que he llamado expandir, con tres fotogramas clave:


     @keyframes expand {
                            from { border-width: 4px; } 
                            50% { border-width: 12px; } 
                            to {
                                  x border-width: 4px;
                                  height: 100%;
                                  width: 100%;
                               }
                       }

Al comienzo de la animación (-), el elemento seleccionado tiene un borde que es 4px ancho; A mitad de la animación (-), el borde aumenta a un ancho de 12 píxeles;y al final de la animación (-), el borde vuelve a4 px de ancho, y la altura y el ancho son ambos 100%.Entre cada uno de los fotogramas clave, los elementos se animan gradualmente, por lo que entre el inicio y la mitad de la animación, el borde se anima para cambiar el ancho suavemente de 4px a 12 píxeles.

Del mismo modo, no es necesario que enumere los selectores de fotogramas clave en orden temporal; poniendo a antes de es perfectamente aceptable, y cualquier conflicto de declaración se resuelve mediante el uso de la cascada: las reglas declaradas más tarde tienen preferencia. Por ejemplo, observe el siguiente conjunto de reglas de fotogramas clave donde se han definido dos fotogramas clave en el mismo punto:

     @keyframes example {
                            10% { background-color: red; }
                            10% { background: green; }
                        }

Cuando se aplica la animación, el color de fondo del elemento será verdeen el 10% punto, ya que se aplicaría la norma declarada más adelante.
Una vez que haya definido los fotogramas clave, el siguiente paso es aplicar propiedades de control de animación a los elementos que desea animar.

## Nombre animación

La propiedad nombre animación se refiere a una animación que se ha definido con @fotogramas clave regla y, como tal, la sintaxis es bastante sencilla:

     E { animation-name: name; }

Puede ver que solo requiere un valor único, que es el nombre de una animación ya definida. Para llamar la animación creada en la sección anterior, usa esto:

     div { animation-name: expand; }

El único otro valor permitido (y el predeterminado) es ninguno,lo que evita que se produzcan animaciones en este elemento.

## Duración de la animación

La duración de una animación la establece el duración de la animación propiedad, que es funcionalmente idéntica a la duración de la transición:

     E { animation-duration: time; }

Al igual que con duración de la transición,el valor tiempo es un número con una unidad de ms o s, o una 0 (cero), lo que impide que se ejecute la animación. (Los valores negativos también se implementan como 0.)Para extender la animación de ejemplo para que tenga una duración de seis segundos, agrega esta línea:

     div { animation-duration: 6s; }

## Función de sincronización de animación

Otra propiedad que debería ser familiar es función de sincronización de animación,que nuevamente es funcionalmente idéntico a su contraparte función de sincronización de transición:

     E { animation-timing-function: value; }

Los valores permitidos son las palabras clave de la función de sincronización (facilidad, lineal, facilidad de entrada, Facilitarse, y facilidad de entrada y salida),el Bézier cúbico()función, o lapasos()función. Por lo tanto, si desea que su animación "se facilite" al principio, agregue este código:

     div { animation-timing-function: ease-in; }

## Retardo de animación

Otra propiedad familiar es retraso de animación,que es idéntica en función a su homólogo, el retraso de transición propiedad:

     E { animation-delay: time; }

Como duración de la animación (y los dos correspondientes transición-*properties), el valor de tiempo es un número con una unidad de ms o s, que establece el retraso antes de que comience una animación. A 0 (cero) significa que no hay demora. Al igual que con duración de la transición,los valores negativos hacen que la animación "salte" esa cantidad.
Para retrasar la animación de ejemplo dos segundos, incluye este código: 

     div { animation-delay: 2s; }

## Animación-iteración-recuento

A diferencia de una transición, que sólo ocurre una vez (o dos, si desea contar al revés), una animación se puede repetir cualquier número de veces. El número de repeticiones lo establece el animación-iteración-recuento propiedad, que tiene esta sintaxis:

     E { animation-iteration-count: count; }

El valor contar en esta sintaxis es un número entero o la palabra clave.infinito. Un valor numérico establece cuántas veces se repite la animación. El valor predeterminado es 1 (uno), lo que significa que la animación se reproduce de principio a fin una vez y luego se detiene. El infinito valor significa que la animación se repite indefinidamente o al menos hasta que se cumpla otra condición que cambie este valor.
Un valor de 0 (cero) o cualquier número negativo impide que se reproduzca la animación.
Para continuar con el ejemplo que he creado a lo largo de esta sección, si quiero que la animación se repita 10 veces, debo agregar la siguiente declaración:

     div { animation-iteration-count: 10; }

## Dirección-animación

Las animaciones se reproducen de principio a fin, pero también pueden reproducirse a la inversa. Puede establecer si su animación se reproduce siempre en una dirección o alterna la reproducción hacia adelante y hacia atrás. Para hacer esto, use el dirección-animación propiedad:

     E { animation-direction: keyword; }

El valor de la palabra clave tiene dos opciones:normal o alterno.El valor predeterminado es normal,que siempre reproduce la animación hacia adelante: la animación se reproduce de principio a fin y luego, si está configurada para repetirse, se reproduce nuevamente desde el principio. Si el alterno se utiliza el valor, la animación se reproduce de principio a fin y luego se reproduce a la inversa antes de comenzar de nuevo. Si considera cada iteración de la animación como un "ciclo", los ciclos impares se reproducen hacia adelante y los pares se reproducen hacia atrás. 
Para completar la animación de ejemplo, configuremos la animación enalterno adelante y hacia atrás:

     div { animation-direction: alternate; }

## Modo de relleno de animación

Si su animación es finita, es decir, si no tiene un valor infinito para el animación-iteración-recuento propiedad—entonces usas el modo de relleno de animación propiedad para establecer cómo aparece el elemento fuera del ciclo de animación. Para mostrarle lo que quiero decir con eso, consideremos las siguientes reglas de estilo:


     @keyframes example {
                            from { background-color: red; }
                            to { background-color: blue; }
                        }

     E{
           animation-delay: 1s;
           animation-duration: 1s;
           animation-iteration-count: 2;
           animation-name: example;
           background-color: green;
       }

En esta regla, elemento mi será verde para el 1s retraso antes de que se active la animación, luego cambie instantáneamente a rojo,luego hacer la transición a azul, iterando dos veces (2),y luego al final volver a la inicialverde.
Puedes cambiar este comportamiento con modo de relleno de animación. La sintaxis se ve así:

     E { animation-fill-mode: keyword; }

Las palabras clave permitidas son ninguno (el valor por defecto),hacia atrás, hacia adelante, o ambos.Si utiliza hacia atrás,las declaraciones especificadas en el 0% (ode) El fotograma clave se aplicará al elemento antes de que comience la animación; si utiliza hacia adelante,las declaraciones en el 100% (oa)el fotograma clave se aplicará cuando finalice la animación; o si usasambos,el 0% Las declaraciones se aplicarán antes de la animación y la 100%,después.

Volviendo al código de ejemplo anterior, si agrega la siguiente regla:

     E { animation-fill-mode: both ; }

entonces elemento mi empezaría rojo,antes de hacer la transición a azuly manteniéndose ese color al final de la animación; es original verde no se aplicaría en ningún momento.

## Animación-reproducir-estado

La propiedad animación-reproducir-estado establece si una animación está activa. Aquí está la sintaxis:

     E { animation-play-state: keyword; }

El valor de la palabra clave tiene dos opciones:correr significa que la animación se está reproduciendo, y pausado significa que no lo es. Puede utilizar esta propiedad para realizar una acción de reproducción/pausa:

     E:hover { animation-play-state: paused; }

En este ejemplo, si se supone que ese elemento mi tiene una animación aplicada, al pasar el mouse sobre el elemento se detiene la animación hasta que se mueve el mouse, momento en el cual la animación continúa.

## La animación Taquigrafía
A lo largo de esta sección, he ensamblado una animación de ejemplo, una propiedad a la vez. Así es como aparecen todas las propiedades combinadas:

     div {
            animation-name: expand;
            animation-duration: 6s;
            animation-timing-function: ease-in;
            animation-delay: 2s;
            animation-iteration-count: 10;
            animation-direction: alternate;
            animation-fill-mode: forwards;
            animation-play-state: running;
         }

Son muchas propiedades que declarar para cada animación. Una vez más, sin embargo, puedes aprovechar una propiedad abreviada llamada animación, y aquí está la sintaxis:

     E { animation: name duration timing-function delay iteration-count direction fill-mode play-state; }

Al igual que con el transición taquigrafía,duración de la animación y retardo de animación deben especificarse en orden. Si alguno de ellos se omite, la sintaxis supone que es retraso de animación,que recibe un valor predeterminado de 0.

Para que el ejemplo que he estado creando en este capítulo sea algo más compacto, puedo usar este código abreviado:

     div { animation: expand 6s ease-in 2s 10 alternate both running; }

Esto todavía puede parecer detallado, pero en su forma más simple, sólo se requieren dos valores para el animación propiedad para funcionar: el nombre del fotograma clave y una duración:

     div { animation: expand 6s; }

Resultados del "Ejemplo 3", del documento Ejemplos_Capitulo14.css subido en el presente repositorio:

El fotograma clave en 0% (-)muestra el elemento con un ancho del bordede 4px y lo heredado altura y ancho (100px cada uno, no mostrados aquí); en el 50% fotograma clave (-), el ancho del borde se incrementa a 12 píxeles;y en la final,100% fotograma clave (-), el ancho del borde regresa a 4pxy tanto la altura como el ancho han cambiado a 100%.

Porque mi dirección-animación el valor es alterno,la animación luego se reproduciría al revés, reduciéndose a sus dimensiones originales, y luego continuaría creciendo y reduciéndose infinitamente debido al valor de animación-iteración-recuento.

![Imagen 2 ilustrando el capitulo 14](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo14/Imagenes/C14/Imagen9_C14.png)

## Múltiples animaciones
Puede agregar varias animaciones a un elemento utilizando una lista separada por comas. Este método funciona para cada una de las sub propiedades y la propiedad abreviada, por lo que ambos ejemplos son válidos:

     E{
         animation-name: first-anim,second-anim; 
         animation-duration: 6s, 1.25ms; 
         animation-delay: 0, 750ms;
      }
      
     E { animation: first-anim 6s, second-anim 1.25ms 750ms; }

Aquí, las listas de valores se repiten para garantizar que todas las propiedades tengan el mismo número de valores aplicados.

