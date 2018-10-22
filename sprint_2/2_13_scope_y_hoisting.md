# Scope y hoisting

<!-- TOC START min:4 max:4 link:true update:true -->
- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)
- [EJERCICIO 3](#ejercicio-3)
- [EJERCICIO 4](#ejercicio-4)

<!-- TOC END -->



## Introducción

A medida que vamos aprendiendo más y más JavaScript, es necesario que vayamos profundizando en conceptos un poco más técnicos pero que es fundamental que entendamos. Estos conceptos nos ayudarán a entender cómo funciona JavaScript a más bajo nivel y harán que captemos mejor el funcionamiento de un código y, por tanto, sepamos resolver mejor los errores que se producen y creemos un código más estable y mejor estructurado.

En esta sesión recordaremos, en primer lugar, qué es el ámbito (scope) de las variables y funciones, y aprenderemos a fondo cómo funciona para tenerlo en cuenta a la hora de ver dónde declarar variables y funciones en nuestro código.

También veremos qué es el hoisting (que no tiene nada que ver con hosting :) ) y que describe cómo reorganiza el intérprete de JavaScript (nuestro navegador web) el código antes de ejecutarlo.


## ¿Para qué sirve lo que vamos a ver en esta sesión?

Hasta ahora hemos establecido una serie de normas porque sí, como que siempre tenemos que declarar una variable antes de usarla o que las funciones las podemos definir después de utilizarlas. También hemos comentado que las variables que creamos fuera de una función pueden usarse dentro de esta y, sin embargo, las que creamos dentro de una función no pueden ser utilizadas fuera de esta.

El hecho es que solo hemos definido reglas para esto y no hemos explicado el porqué detrás de cada una de ellas. Lo que vamos a ver en esta sesión nos ayudará a saber el por qué y a conocer cuál es el proceso que se produce en nuestro navegador y que influye en ese comportamiento.


## ¿En qué casos se utiliza?

Dado que todo lo que vamos a ver es algo relacionado con cómo funciona JavaScript, nos será útil en todo momento debido a que estos conceptos forman parte de la naturaleza de este lenguaje.

Aprender este tipo de conceptos un poco más avanzados te aportará conocimientos clave a la hora de empezar a trabajar con JavaScript y a obtener una base sólida y unos conocimientos que van más allá de generar código sin saber las reglas que caracterizan la estructura, entender el por qué detrás de ciertas buenas prácticas.


## Ámbito o scope

Bien, vamos a empezar recordando qué es aquello del  ámbito o _scope_. 
Usamos `let` y `const` para definir nuestras variables, y por defecto tienen ámbito de bloque (un bloque es cualquier expresión con llaves `{}`, como un `if`, `for`, `function`).

Partamos del siguiente código:
```js
const a = 'Hi, I\'m A';

if (true) {
  let b = 'I am true just here';
}

for (let c=0; c<10; c++) {
  console.log('>>', c);
}

function f() {
  const d = 'Help, I\'m a prisoner';
}
```

- **a**, es una variable global, está definida en el ámbito superior de nuestro programa y accesible para todo el mundo.
- **b** y **c**, son variables locales, cuyo ámbito o scope es el bloque donde están definidas, fuera de ese bloque no existen. **Vamos a tener especial cuidado en no definir variables dentro de un `if`**.
- **d**, es una variable local muy común, existe dentro de la función y no está accesible fuera de ella.

Veamos otro ejemplo:

```js

let greeting = 'Hola';

function sayHello() {
  let greeting = 'Hello';
  console.log(greeting);
}

sayHello();
```

>Como puedes ver, este código no tiene ninguna lógica, simplemente es algo sencillo para que nos sirva de ejemplo.

¿Sabrías adivinar que va a mostrar? Piénsalo detenidamente (no vale ejecutar el código 👮🏼‍♀️).

Bien, antes de saber cuál será el resultado, vamos a ver qué pasos sigue este código.

JavaScript en este caso realiza los siguientes pasos:
1. Genera la variable `greeting` en el ámbito global y  le asigna `Hola`
1. Declara una función (crea la función)
1. Ejecuta la función sayHello
1. Al ejecutar la función `sayHello` y por tanto el código que contiene, se crea una variable `greeting` en el ámbito de la función `sayHello`
1. Se ejecuta el `console.log`, en este caso como le hemos pasado como argumento la variable `greeting`, buscará esa variable en el ámbito más próximo y utilizará el valor que almacena

Recordemos que en JavaScript, el ámbito (o scope) se encarga de llevar la lista de todas las variables y funciones declaradas y define una serie de reglas que establecen si esas variables son accesibles en el momento de ejecutar un código.

Como esto puede ser un poco lioso, vamos a ilustrar cuáles serían los ámbitos en el ejemplo anterior, cómo funcionan y cómo se modifican en cada paso.

Bien, volviendo a los pasos anteriores, vamos a ilustrar cada uno de ellos para ver que sucede:

### 1. Genera la variable `greeting` en el ámbito global y le asigna `Hola`

En este paso añadimos al *scope* global una variable `greeting` y guardamos el valor de `Hola` dentro de ella. El ámbito global abarcaría todo el código, como hemos comentado anteriormente, si generamos una variable o función en el scope global esta podrá ser usada en cualquier parte de nuestro JavaScript, de ahí que el alcance de este scope (donde se pueden utilizar las variables y funciones creadas en él) se extienda a todo el código.

### 2. Declara una función (crea la función)

Al crear la función `sayHello`, generamos un nuevo ámbito, por lo que todas las variables que se creen dentro de la función ya no estarán incluidas en el ámbito global, sino en el de esta función. Lo mismo sucede con los parámetros, que estarán incluidos en el ámbito.

### 3. Al ejecutar la función `sayHello` y por tanto el código que contiene, se crea una variable `greeting` en el ámbito de la función `sayHello`

Bien, hemos creado una variable y la hemos creado dentro de `sayHello`. En el momento de crearla, esta se añadirá al scope de la función.

### 4. Se ejecuta el `console.log`, en este caso como le hemos pasado como argumento la variable `greeting`, buscará esa variable en el ámbito más próximo y utilizará el valor que almacena

Bien, este es una de las partes clave para entender cómo funciona el scope. En esta parte del código estamos utilizando la variable `greeting` para poder utilizar el valor que almacena y por tanto, que este se muestre en el `console.log`. ¿Qué hace JavaScript en este caso? Pues muy simple, busca si esa variable existe en el ámbito actual y sino en el ámbito que está por encima y sino en el de encima de ese y así continuamente.

En este caso busca en el ámbito actual, como el código se está ejecutando dentro de la función `sayHello`, el ámbito actual será el ámbito de la función, por lo que en primer lugar buscará ahí si existe la variable que necesita (`greeting`). Como sí existe ahí, utiliza esa variable para coger el valor y por tanto, como en este caso el `greeting` de dentro de la función guarda `'Hello'`, se sustituirá por ese texto y el `console.log` mostrará `'Hello'`.

Si en este caso no hubiésemos declarado una variable `greeting` en la función, al ejecutar el código, el intérprete de JavaScript (el navegador) buscaría esa variable en el ámbito de `sayHello` y al no encontrarla iría subiendo en ámbitos. En ese caso iría directamente al ámbito global porque es el único por encima de `sayHello` y trataría de buscar ahí la variable. Como ese scope tiene una variable `greeting` definida, utilizará esa y por tanto en este caso el `console.log` mostrará `'Hola'`.

Si tras buscar en todos los ámbitos que afectan a un código no se encuentra ninguna variable que coincida con la utilizada, se producirá un error de JavaScript llamado `ReferenceError` porque no encuentra la referencia a la variable utilizada, no encuentra ningún sitio donde se haya declarado esa variable y por tanto hay un error de referencia (porque la referencia no existe).

El scope es algo que no podemos ver pero que debemos tener en cuenta y entender para prever cuál será el resultado de nuestro código. Es un proceso que no vemos pero está ahí y existe e influye en cómo se ejecuta el código.

## Consultar el scope en las Chrome DevTools

Por último, podemos saber cual es el scope local y global en un momento determinado utilizando la pestaña *Sources* de las Chrome Dev Tools. Esta pestaña sirve para depurar nuestro código JavaScript y comprobar qué está haciendo en cada paso. En ella nos aparece un panel a la izquierda de la pantalla con la estructura de carpetas de la página. Si no nos aparece el panel, tenemos que pulsar en el icono con la flecha que apunta hacia la derecha, situado justo debajo del icono con el ratón.

>Vista por defecto de la pestaña de _Sources_ de las Chrome DevTools

![Pestaña de _Sources_ de las herramientas de desarrollo de Chrome](assets/images/3-6/empty-devtools-sources-tab.png)

A continuación seleccionaremos el archivo JavaScript que queremos depurar dentro de la estructura de carpetas y nos mostrará el código del archivo.

>Vista con un archivo abierto. Pestaña de _Sources_ de las herramientas de desarrollo de Chrome

![Pestaña de _Sources_ con un archivo abierto](assets/images/3-6/devtools-sources-tab.png)

Para comprobar cuál es el scope en un momento determinado de la ejecución de nuestro código, simplemente pulsamos en el número de una línea de código para generar una parada en el código (*breakpoint*), al pulsar sobre el número aparecerá un marcador azul para indicarnos que hemos generado una parada.

>Código con un *breakpoint* para parar la ejecución en una línea determinada

![Código con un breakpoint para parar la ejecución en una línea determinada](assets/images/3-6/how-to-add-breakpoint-sources.png)

Después de generar una parada en el código, recargamos la página. Al recargarla ejecutará el código JavaScript hasta la linea en la que hemos puesto el breakpoint, donde se parará hasta que le digamos que continue.

>Vista del código parado en un punto determinado

![Vista del código parado en un punto determinado](assets/images/3-6/javascript-execution-paused.png)

En este momento podemos ver a la derecha un panel con una sección que tiene el nombre de *Scope*. Dentro de esta podremos ver otras dos subsecciones, local y global. Local hará referencia al scope local (si se está ejecutando una función, será al scope de la función) y global hará referencia al scope global, a todas las variables y funciones disponibles a lo largo de todo nuestro código (tanto las que hemos creado nosotros como las que genera por defecto el navegador). El scope que se muestra será el que haya justo en el momento antes de ejecutar la linea de código en la que hemos realizado la parada.

>Vista de la sección scope en el panel de info de Sources

![Vista de la sección scope en el panel de info de Sources](assets/images/3-6/scope-section.png)

Y hasta aquí sería la descripción de qué es el scope o ámbito en JavaScript. Si no te ha quedado todo perfectamente claro y no lo has pillado a la primera no te preocupes, este concepto es algo que a veces cuesta más, la idea es explicarlo y que, a base de consultarlo y volver de vez en cuando a esta explicación se llegue a un punto de entendimiento del concepto. Por el momento, con entender que el scope determina el alcance de nuestras variables y funciones y como funciona a grandes rasgos es más que suficiente. La práctica y repaso a base de constancia con el código harán el resto para entender a fondo de qué se trata.

* * *

#### EJERCICIO 1

**Averigua el resultado**

A continuación vamos a poner una serie de códigos. Estos no tienen un sentido lógico más allá de practicar con lo aprendido sobre el scope. Sin ejecutarlos, intenta averiguar qué se mostrará en el `console.log` de cada uno de ellos.

>NOTA: Los ejercicios son parecidos pero cada uno de ellos tiene una modificación. Lo mejor es leer paso a paso qué hace cada uno, aunque ya lo hayamos leído antes, para saber cuál será el proceso que realicen.

```js
let message = 'El resultado será A';

function changeMessage() {
  message = 'El resultado será B';
}

changeMessage();

console.log(message);
```

```js
let message = 'El resultado será A';

function changeMessage() {
  message = 'El resultado será B';
}

console.log(message);
```

```js
let message = 'El resultado será A';

function changeMessage() {
  let message = 'El resultado será B';
}

changeMessage();

console.log(message);
```

Una vez hayas intentado averiguar cuál es el resultado de estos código, comprueba si has acertado o no ejecutándolos en tu navegador.

* * *

#### EJERCICIO 2

**Aprendiendo a averiguar el scope con las Dev Tools**

Abre tu ejercicio de evaluación individual del segundo sprint (el de adivinar el número aleatorio) y después abre el panel de las Chrome Dev Tools. Selecciona la pestaña _Sources_, coloca algunas paradas en el código pulsando en los números de línea del editor de código que aparece. Recarga la página para que se vaya parando en cada una de las líneas y comprueba en el panel derecho cual es el scope en cada caso.

Prueba a poner paradas tanto dentro de funciones como fuera para ver qué sucede.

* * *

## Hoisting

Como hemos visto hasta ahora, JavaScript genera ámbitos para determinadas partes de nuestro código, una cosa que hace para que la tarea de generar esos ámbitos sea más rápida es que todas las declaraciones de funciones se "mueven" al principio de su ámbito respectivo, esto es a lo que llamamos _hoisting_.

Imaginemos que tenemos el siguiente código:

```js
const lower = 1;
const upper = 100;

const randomNumber = getRandomNumber(lower, upper);

function getRandomNumber(min, max) {
  console.log('Vamos a crear un número random');

  const message = 'Se ha generado un número aleatorio: ';
  const result = Math.floor((Math.random() * (max - min)) + min);

  console.log(message + result);

  return result;
}
```

Podemos usar la función `getRandomNumber()` antes de declararla gracias a que JavaScript cambiará el orden del código y lo dejará de la siguiente forma:

```js
function getRandomNumber(min, max) {
  console.log('Vamos a crear un número random');

  const message = 'Se ha generado un número aleatorio: ';
  const result = Math.floor((Math.random() * (max - min)) + min);

  console.log(message + result);

  return result;
}

const lower = 1;
const upper = 100;

const randomNumber = getRandomNumber(lower, upper);
```

Como se puede ver, lo que hace básicamente es mover las declaraciones de funciones del scope.

¡OJO! En el caso de las variables definidas con `const` y `let` el hoisting no se aplica de manera que se crean y se asignan cuando aparecen en nuestro código. Por eso siempre se recomienda que antes de usar una variable siempre la declaremos y asignemos, para que en el momento de usarla ya tenga un valor definido.

Saber esto nos ayuda a entender varias cosas:
- Las funciones siempre se van a mover arriba, por lo que da igual dónde las declaremos (antes o después de usarlas) siempre podremos usarlas donde queramos
- Las declaraciones de variables con `const` y `let` no se mueven: debemos tener cuidado de siempre crear y asignar una variable antes de usarla
- JavaScript realiza una serie de operaciones antes de ejecutar el código, estas le facilitan el trabajo y optimizan la ejecución del código

Recordemos que hay otra forma de escribir funciones y es asignando funciones anónimas a variables:

```js
const sum = function(a,b) {
  return a+b;
}
```
O usando funciones flecha:
```js
const sum = (a,b) => a+b
```

Aquí se aplicarían las mismas reglas de hoisting que se aplican a `const` y `let` por lo que NO podríamos ejecutar el siguiente código:

```js
console.log(sum(2,3));
const sum = (a,b) = a+b;
```

mientras que con el anterior sistema de escritura de funciones sí podríamos ya que el hoisting de Javascript transformaría este código:

```js
console.log(sum(2,3));
function sum(a,b) {
  return a+b;
}
```

en este otro:

```js
function sum(a,b) {
  return a+b;
}
console.log(sum(2,3));
```

* * *

#### EJERCICIO 3

**Comprobando cómo se aplica el hoisting con las Chrome Dev Tools**

Abre tu ejercicio de evaluación individual del segundo sprint (el de adivinar el número aleatorio). Pon una parada en el código y comprueba si las variables se han añadido al scope para ver cómo JavaScript aplica el _hoisting_.

* * *

#### EJERCICIO 4

**Detectando fallos en las declaraciones de variables**

A continuación vamos a poner una serie de códigos, algunos de ellos tendrán un error debido a que hemos usado/modificado una variable en un ámbito que no está definido. Averigua cuáles de estos códigos son los que tienen un error e intenta razonar el por qué.

>NOTA: Estos códigos no tienen un sentido lógico más allá de practicar con lo aprendido sobre el scope

```js
'use strict';

const message = '¡Hola!';
function showMessage() {
  console.log(message);
}
showMessage();
```

```js
'use strict';

function showMessage() {
  console.log(message);
}
showMessage();
const message = '¡Hola!';
```

```js
'use strict';

let message;

function showMessage() {
  console.log(message);
}
showMessage();
message = '¡Hola!';
showMessage();
```

```js
'use strict';

message = '¡Hola!';

function showMessage() {
  console.log(message);
}
showMessage();
```

```js
'use strict';

function showMessage() {
  let message = '¡Hola!';
  console.log(message);
}

let message = 'Hello';
showMessage();
```

* * *
