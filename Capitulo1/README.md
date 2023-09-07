# INTRODUCING CSS3

## ¿Qué es CSS3 y cómo surgio?

El trabajo en CSS3 comenzó en 1998, el año siguiente a la publicación de CSS2. Sin embargo, la implementación de CSS2 en los navegadores seguía siendo tan frustrantemente 
inconsistente que el W3C decidió detener el trabajo en una nueva revisión y trabajar en CSS2.

En 2005, todos los módulos de CSS3 volvieron al estado de borrador de trabajo, y el proceso de edición y revisión comenzó de nuevo.

Cada uno de los navegadores quiere ofrecer a desarrolladores y usuarios lo último en tecnologías web, y con la especificación CSS3 ya redactada en su mayor parte, implementar
e incluso  añadir nuevas funciones ha sido pan comido.

## CSS3 es modular
Los miembros del W3C, conscientes de que no querían retrasar algunas de las características más obvias y demandadas mientras consideraban y debatían algunas de las más 
esotéricas tomó la decisión de dividir CSS3 en varios módulos. Así, cada uno de los módulos podría ser trabajado por distintos autores a ritmos diferentes, y el proceso 
de implementación y recomendación podría escalonarse.
 
Esta es la razón por la que, en lugar de un documento único y monolítico sobre la especificación CSS3, tenemos el Módulo de Interfaz de Usuario Básica de CSS3, Selectores de 
Nivel 3, Consultas de Medios, etc.

### Estado del módulo y proceso de recomendación
El estado lo establece el W3C, e indica el progreso del módulo en el proceso de recomendación; sin  embargo, ten en cuenta que el estado no es necesariamente una indicación
del grado de implementación de un módulo en cualquier navegador.

Cuando un documento propuesto se acepta por primera vez como parte de CSS3, su estado se designa como borrador de trabajo. Este estado significa que el documento ha sido
publicado y está listo para ser revisado por la comunidad.

Un documento puede permanecer como borrador de trabajo durante un largo periodo de tiempo y someterse a numerosas revisiones. No todos los documentos superan este nivel de 
estado, y un documento puede volver a este estado en muchas ocasiones; Antes de que un documento pueda pasar de Borrador de Trabajo, su estado cambia a Última Llamada, lo que significa que el periodo de revisión está a punto de cerrarse y suele 
indicar que el documento está listo para pasar al siguiente nivel.

El siguiente nivel es el de Recomendación Candidata, lo que significa que el W3C considera que el documento tiene sentido, que las últimas revisiones no han encontrado
problemas significativos y que se han cumplido todos los requisitos técnicos. 

Cuando dos o más navegadores hayan implementado las propiedades de la misma manera y si no han surgido problemas técnicos graves, el documento puede pasar a ser una
Recomendación propuesta. Este estatus significa que la propuesta ya está madura e implementada y lista para ser aprobada por el Comité Asesor del W3C. 
Una vez obtenida esta aprobación, la propuesta se convierte en Recomendación.

Un módulo puede estar bien implementado en todos los navegadores y, sin embargo, tener el estatus de borrador de trabajo: el módulo Transitions (capítulo 14) tiene
exactamente ese estatus. A la inversa, un módulo puede tener el estado de Recomendación de candidato y, sin embargo, tener una implementación limitada: Shapes de CSS
(capítulo 19) se ajusta a esta descripción en este momento.

## No hay CSS3
Como CSS se ha vuelto modular, a cada módulo se le asigna un n ú m e r o de nivel para marcar el número de revisiones por las que ha pasado. 
CSS3 es simplemente una abreviatura conveniente para significar "características CSS desarrolladas desde CSS2.1". 
Con el tiempo, la numeración desaparecerá y sólo tendremos CSS, con módulos a diferentes niveles.

## Introducción a la sintaxis

***E { propiedad: valor; }***

En este ejemplo de código, el selector se representa con E. Por supuesto, en HTML, este selector no existe; simplemente lo estoy 
utilizando para indicar que el selector es irrelevante; aquí se podría utilizar cualquier selector.
A continuación, tienes la propiedad en sí; en este caso, he utilizado una propiedad inventada, llamada propiedad. A continuación está
el valor de la propiedad. Para ello, utilizo un alias en cursiva para referirme al valor, que en este caso he llamado valor.

Si una propiedad acepta múltiples valores, listaré cada uno con un alias único. Así que una nueva propiedad que requiere tres 
valores podría definirse así:

***E { propiedad: primero segundo tercero; }***

Dicho esto, imaginemos que tenemos una nueva propiedad llamada monos (siempre he querido una propiedad monos), que sólo acepta un único
valor. Usando la sintaxis de este libro, la introduciría así:

***E { monos: valor; }*** 

Y a la hora de ofrecer un ejemplo práctico de ello, podría mostrarlo con un valor válido -digamos, un valor numérico- como éste:

***E { monos: 12; }***

## Prefijos de proveedores

Cuando un módulo está aún en revisión activa, como es el caso de CSS3, muchas cosas pueden cambiar; la sintaxis de una propiedad puede 
ser revisada, o una propiedad puede ser eliminada por completo. En ocasiones, incluso la redacción del propio borrador puede ser un 
poco nebulosa y abierta a la interpretación.
cada uno de los proveedores de navegadores comenzó a anteponer un código corto al principio de las propiedades experimentales. 
Imaginemos que nuestra tan deseada propiedad monos ha sido recientemente definida en una especificación, y que todos los principales 
proveedores de navegadores han decidido implementarla para ver cómo funciona. En este caso, se utilizaría el siguiente código:

***E {
-moz-monkeys: value; /* Firefox */***

***-ms-monkeys: value; /* Internet Explorer */***

***-webkit-monkeys: value; /* Chrome/Safari */
}***

Aunque bienintencionado, el uso de prefijos de proveedor ha dado lugar a muchos problemas: los desarrolladores los utilizaban en sus
sitios web de producción, pero no los eliminaban más tarde, cuando la implementación del navegador había cambiado. Esto, a su vez,
significaba que los proveedores de navegadores tenían que seguir dando soporte a las funciones experimentales para evitar fallos en 
los sitios web que las utilizaban. Por este motivo, Chrome y Firefox están dejando de utilizar propiedades prefijadas y prefieren 
implementar nuevas funciones que estén  desactivadas por defecto y que los desarrolladores tengan que aceptar hasta que sean lo 
suficientemente estables para su uso generalizada





