# SELECTORES

![Imagen ilustrando el capitulo2](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo3/Imagenes/CSS_Selectors_650x3501.jpeg)

Los selectores son el corazón de CSS, y aunque la especificación CSS1 original solo anunciaba 5 "h", CSS2 amplió el rango con 12 más. 
Los selectores se pueden dividir en términos generales en dos categorías:

1.Los primeros son aquellos que actúan directamente sobre los elementos definidos en el árbol del documento (pag elementos y href atributos).

2.La segunda categoría contiene pseudo-selectores que actúan sobre elementos o información que se encuentran fuera del árbol del documento
(como la primera letra de un párrafo o el último hijo de un elemento principal). 

CSS3 proporciona tres nuevos selectores de atributos y uno nuevo combinador. 

## Selectores de atributos

Los selectores de atributos se introdujeron en CSS2 y, como es de esperar por el nombre, le permiten especificar reglas que coinciden con 
elementos en función de sus atributos, como href o título y los valores de esos atributos. 

Los cuatro selectores definidos en CSS2 son:

    E[atributo] {...} /* Selector de atributos simple */ 
    E[atributo='valor'] {...} /* Selector de valor de atributo exacto */ 
    E[ atributo~='valor'] {...} /* Selector de valor de atributo parcial */ 
    E[ atributo|='valor'] {...} /* Selector de atributos de idioma */


* El **Selector de atributos simple** aplica reglas a elementos que tienen definido el atributo especificado, independientemente del valor de ese
atributo, ver “Ejemplo 1: Selector de Atributos simple” del archivo de CSS(Ejemplos_Capitulo3) cargado en Capitulo3 del presente repositorio. 

* Si quieres ser más específico, puedes utilizar el **Selector de valor de atributo exacto** para definir un valor, este selecciona solo 
elementos que tienen el valor exacto establecido, ver “Ejemplo 2: Selector de valor de atributo exacto” del archivo de CSS(Ejemplos_Capitulo3)
cargado en Capitulo3 del presente repositorio.

* El **Selector de valor de atributo parcial** busca el valor como parte de una lista separada por espacios (en la mayoría de los casos, una 
palabra) y así aplica la regla a los elementos, sin importar si coincide exactamente o contiene más palabras, ver “Ejemplo 3: Selector de valor
de atributo parcial” del archivo de CSS(Ejemplos_Capitulo3) cargado en Capitulo3 del presente repositorio.

* **El Selector de atributos de idioma**, aplica reglas a elementos que tienen un atributo que coincide con el primer argumento del selector,
seguido inmediatamente por un guión. Si eso suena extrañamente específico, es porque este selector en realidad solo está destinado a
coincidir con subcódigos de idioma, ver “Ejemplo 4: Selector de atributos de idioma” del archivo de CSS(Ejemplos_Capitulo3) cargado en
Capitulo3 del presente repositorio.
 
## Nuevos selectores de atributos en CSS3.

Los nuevos selectores de CSS3 brindan flexibilidad con el poder de hacer coincidir subcadenas dentro de un valor de atributo. 
Esta característica los hace especialmente buenos para aplicar reglas a documentos XML, que a menudo pueden tener valores de atributos más 
variados que HTML, aunque también siguen siendo bastante útiles para los desarrolladores de HTML.

### **Selector de valor de atributo de subcadena inicial**
El Selector de inicio: busca elementos cuyo atributo elegido comienza con la cadena proporcionada como argumento. Utiliza el símbolo de
intercalación (^) para modificar el signo igual en el selector. Aquí está la sintaxis completa:

    E[atributo^='valor'] {...}
 
Este código busca el valor proporcionado al principio del atributo especificado y es especialmente útil cuando desea agregar información visual 
a los hipervínculos, ver “Ejemplo 5: Selector de valor de atributo de subcadena inicial”, "Ejemplo 5.1: Selector de valor de atributo de 
subcadena inicial" y " Ejemplo 5.2: Selector de valor de atributo de subcadena inicial" del archivo de CSS(Ejemplos_Capitulo3) cargado en
Capitulo3 del presente repositorio.


![Resultados Ejemplo 5.1](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo3/Imagenes/Ejemplo%205.1.png)
***Imagen 1: Resultados del Ejemplo 5.1***

![Resultados Ejemplo 5.2](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo3/Imagenes/Ejemplo%205.2.png)
***Imagen 2: Resultados del Ejemplo 5.2*** 



### **Selector de valor de atributo de subcadena final**
El Selector de final, como yo lo llamo, funciona exactamente igual que el Selector de inicio, ¡sólo al revés! Es decir, lo utilizas para
seleccionar atributos que fin con el valor suministrado. La sintaxis difiere solo en un carácter: esta vez usa el carácter del signo de dólar 
($) para modificar el signo igual (=). Aquí está la sintaxis completa:

    E[atributo$='valor'] {...}
 
Al igual que el selector de inicio, puede utilizar este selector para proporcionar claridad visual a los hipervínculos. Pero esta vez, en lugar 
de utilizar los protocolos al principio del href atributo, utiliza los tipos de archivos al final, ver “Ejemplo 6: Selector de valor de atributo
de subcadena inicial” y "Ejemplo 6.1: Selector de valor de atributo de subcadena final" del archivo de CSS(Ejemplos_Capitulo3) cargado en
Capitulo3 del presente repositorio.

![Resultados Ejemplo 6.1](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo3/Imagenes/Ejemplo%206.1.png)
***Imagen 3: Resultados del Ejemplo 6.1*** 



### **Selector de valor de atributo de subcadena arbitrario**

El último selector de nuevos atributos, al que yo llamo Selector arbitrario—Funciona de la misma manera que los dos anteriores, pero busca el
valor de subcadena proporcionado, en cualquier lugar dentro de la cadena de atributo especificada. Este selector utiliza el carácter asterisco 
(*). Aquí está la nueva sintaxis:

    E[atributo*='valor'] {...}
 

Este selector es el más flexible de los tres nuevos selectores de atributos, ya que puede hacer coincidir subcadenas sin importar dónde 
aparezcan dentro de las cadenas. Pero esta flexibilidad adicional significa que debes tener más cuidado al definir los valores proporcionados
al selector, ver “Ejemplo 7: Selector de valor de atributo de subcadena arbitrario” del archivo de CSS(Ejemplos_Capitulo3) cargado en
Capitulo3 del presente repositorio.

### **Selectores de atributos múltiples**

También puedes encadenar varios selectores, lo que te permite ser realmente específico. Usando múltiples selectores, puede crear reglas para
aplicar a atributos con valores definidos para el inicio, el final y cualquier punto intermedio, ver “Ejemplo 8: Selectores de atributos 
múltiples” del archivo de CSS(Ejemplos_Capitulo3) cargado en Capitulo3 del presente repositorio. 

### **El combinador general de hermanos**

Nuestro último selector DOM nuevo en CSS3 es un combinador, que como recordará significa que une más de un selector. El Combinador general de
hermanos es una extensión del Combinador de hermanos adyacentes, que se introdujo en CSS2. Las sintaxis difieren en un solo carácter:

    E+F{...} /*Combinador de hermanos adyacentes */ 
    E~F{...} /*Combinador general de hermanos */
    
La diferencia entre los dos es sutil pero importante: el hermano adyacente selecciona cualquier elemento (F) que está inmediatamente precedido 
por el elemento (E) en el mismo nivel del árbol del documento, pero General selecciona cualquier elemento (F) que está precedido por el 
elemento (E) en el mismo nivel del árbol, independientemente de si es inmediatamente adyacente, ver “Ejemplo 9: Combinador general de hermanos”
del archivo de CSS(Ejemplos_Capitulo3) cargado en Capitulo3 del presente repositorio. 

![Resultados Ejemplo 9](https://github.com/ElizaMejia/Curso-CSS/blob/Capitulo3/Imagenes/Ejemplo%209.png)
***Imagen 4: Resultados del Ejemplo 9***

