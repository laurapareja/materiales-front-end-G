# Introducción a la programación 2

<!--@TODO intro-->

## La consola de JavaScript

En las herramientas para desarrolladoras de Chrome (las DevTools) hay una pestaña que es una consola JavaScript. La consola nos permite escribir instrucciones JavaScript que al dar al Enter se ejecutan. En la consola puedes probar a hacer sumas, declarar variables, funciones, etc.

<!--@TODO ejercicio con let o const directamente en consola-->
* * *
#### EJERCICIO 1

* * *

Con la consola también podemos interactuar desde nuestro programa JavaScript, es decir, desde el código que escribimos en nuestro fichero `.js`. Una de las cosas que podemos hacer es escribir información, esto se denomina comúnmente *loguear* información. Lo hacemos mediante la función `console.log()` en la que lo que pongamos entre paréntesis será lo que se escriba en la consola. 

```js
console.log('Hola');

const age = 56;
console.log(age);
```

A priori puede parecer que esto no tiene mucha utilidad ya que en nuestra página web no veremos nada, solo si abrimos las herramientas de desarrolladores. Pero vas a ir comprobando lo útil que es, por ejemplo, para depurar (resolver) errores en el código, o para hacer "trazas" de operaciones y asegurarnos de que todo funciona como esperamos antes de, por ejemplo, modificar el HTML.

```js
const welcomeParagraph = document.querySelector('.welcomeText');

// Logueo el contenido de la constante welcomeParagraph en la consola y compruebo que tiene asignado el elemento de HTML que espero
console.log('welcomeParagraph: ', welcomeParagraph);

welcomeParagraph.innerHTML = 'Bienvenida Adalaber';
```

La consola del navegador es a JavaScript lo que el inspector de elementos a HTML y CSS, es decir, herramientas indispensables para desarrollar.

A partir de ahora cada vez que escribamos código JavaScript y sirvamos nuestra página en el navegador, por defecto abriremos la consola, ya que sin ella estaremos programando "a ciegas".

<!--@TODO ejercicio con querySelector y una clase con una errata + console.log ¿¿??-->
* * *
#### EJERCICIO 2

* * *

## Tipos de datos

En la sesión anterior hablamos de que programar es básicamente realizar operaciones sobre datos para obtener un resultado concreto. Bien, esos datos con los que trabajamos en nuestro código se representan mediante valores. Por tanto un valor no es más que la representación de un dato sobre la que podemos aplicar las reglas comentadas anteriormente. Si queremos mostrar la temperatura en una pantalla, necesitaremos el valor numérico (por ejemplo, 27) que represente el dato de esa temperatura y sobre ese valor aplicaremos las reglas para obtener el resultado deseado (sacar la media de temperatura, calcular el día que más calor ha hecho, etc.).

Se aprecia con esto que la base de la información de nuestra aplicación reside en los valores. Éstos serán los encargados de representar los datos y serán sobre los que apliquemos las operaciones necesarias.

En JavaScript existen por defecto siete tipos distintos de datos, casi todos ellos los veremos a lo largo del curso, pero por el momento vamos a centrarnos en tres: `string` (cadena de caracteres), `number` (número) y `boolean` (booleano).

Cada uno de ellos, según sus características, se utilizará para representar un tipo de valor concreto. El tipo `number`, como habrás podido deducir, se utilizará para representar números, el tipo `string` se utilizará para representar texto, compuesto de varios caracteres que unidos entre sí forman una cadena (string), y el tipo `boolean` para representar verdadero o falso.

### Number

Cómo su nombre indica, el tipo de valor _number_ comprende cualquier tipo de número utilizado en JavaScript. Hay varios subtipos de números en JavaScript pero de momento aprenderemos los más importantes, números enteros o _integers_ y números decimales o _floating point numbers_.

En JavaScript los números enteros se representan directamente con cifras, por lo que es totalmente válido escribir `14232` o `-42` en nuestro código. Por otro lado, los números decimales se escriben igual que en inglés, es decir, utilizando puntos en vez de comas. Por ejemplo, podemos representar el número _1,32_ escribiendo `1.32`.

Las anteriores son las únicas reglas gramaticales a la hora de escribir números enteros y decimales. Pero escribir números sin hacer nada con ellos no tiene ninguna utilidad, lo que queremos es poder obtener otros números, es decir, poder operar con ellos. Esto lo podemos conseguir mediante los operadores de suma, resta, multiplicación, división y módulo.


### Suma, resta, multiplicación y división

En JavaScript, los operadores de suma (`+`), resta (`-`), multiplicación (`*`) y división (`/`) se utiliza exactamente igual que en matemáticas.

```js
1 + 2        // Devuelve 3
1.4 - 2.4    // Devuelve -1
+ 7          // Devuelve 7
-40          // Devuelve -40
-+8          // Devuelve -8
30 + 20 - 4  // Devuelve 46
3 + 3 + 3    // Devuelve 9

4 * 4        // Devuelve 16
8 * -7       // Devuelve -56
4 * 2 / 8    // Devuelve 1
0 / 8        // Devuelve 0
1.6 / 0.2    // Devuelve 8
```

**Nota:** El espacio entre los números no es necesario, podríamos poner `4+4` y funcionaría perfectamente. La finalidad de ese espacio es ayudar a visualizar mejor el código y la mayoría de los programadores en JavaScript suelen utilizarlos, por tanto, nosotros también lo haremos así.

El orden en el que se ejecutan los operadores también es igual que el utilizado en matemáticas. De izquierda a derecha y evaluándolos en el siguiente orden:

1. Operaciones entre paréntesis.
2. Multiplicación y división.
3. Suma y resta.

Los paréntesis en JavaScript, a la hora de aplicarlos a los números, funcionan igual que en matemáticas.

```js
4 + 4 * 4 / 8     // Devuelve 6
(4 + 4) * 4 / 8   // Devuelve 4
(4 + 4) * (4 / 8) // Devuelve 4 también
```


* * *
#### EJERCICIO 3

El precio de la fruta

Imagina que vamos a la frutería y compramos lo siguiente:

- 2 kilos de kiwis a 5€/kg
- 3 kilos de peras conferencia (no una cualquiera) a 2€/kg
- medio kilo de uvas a 4€/kg

Con lo que hemos visto durante los ejemplos y textos anteriores y usando JavaScript, vamos a calcular el precio total como si lo hiciésemos en una hoja de toda la vida pero de manera mucho más guay. El resultado debe mostrarse en la consola del navegador.

* * *

#### EJERCICIO 4

¡Págame, tía!

Nos vamos de cena de Navidad, ¡qué alegría! Somos en total 9 personas y la cuenta del restaurante japonés es de 128€. Ana tiene que pagar 2€ más que los demás porque ha pedido un chupito de sake. ¿Cuánto tenemos que pagar cada una? ¿Y Ana? Hagamos un pequeño programa en JavaScript para calcularlo. El resultado debe mostrarse en la consola del navegador.


* * *
#### EJERCICIO 5

Calcular el número total de horas que hemos vivido

En este caso vamos a crear un código que nos diga cuantas horas en total hemos vivido. Por ejemplo, si alguien tiene 60 años, este código debería de mostrar un mensaje con el número "525600".

**Nota:** En este caso no tendremos en cuenta los años bisiestos para no complicar mucho el ejercicio.
* * *

### String

_String_ traducido al español significa cadena y como su nombre indica es el tipo de valor utilizado para representar cadenas de caracteres, que viene a ser básicamente texto. Cualquier tipo de texto, ya sean caracteres sueltos ("a", "b", "0") o en conjunto ("hola", "las 13:40", "2312312") estará incluido dentro de este tipo de valor.

En los ejercicios anteriores, siempre que hemos escrito entre comillas (`''`) un texto, lo que hemos hecho es incluir en el código un _string_, decirle al programa encargado de ejecutar nuestro código que eso es un texto y que debe utilizarlo como tal en vez de entenderlo como una orden (como hace con `console.log` o con `document.querySelector`).

Para representar un string en JavaScript, se puede utilizar tanto texto envuelto entre comillas simples (`''`) como dobles (`""`). Ambas son totalmente válidas y funcionan de la misma manera salvo que las comillas simples no pueden contener dentro otras comillas simples y las dobles no pueden contener dobles. De esta forma, `'Esto es un 'bug''` da error porque el navegador al ejecutar el código entiende que un texto termina antes de `bug` y comienza otro texto después de `bug`. Pasaría lo mismo si usamos `"Esto es un "bug""`.

Para evitar estos errores producidos por el uso de comillas anidadas existen dos soluciones:
- Usar comillas simples siempre que el texto contenga comillas dobles o viceversa
- Usar la barra inclinada (`\`) delante de las comillas anidadas (Ej: `'I\'m a front-end developer'`). De esta forma decimos a JavaScript que esas comillas son texto normal y no van a ser usadas para marcar el final del string y por tanto no se produce el error.

Otra regla es que debe coincidir el estilo de la comilla de apertura con la de cierre:

```
'esto es un texto válido'
'esto no es válido"
```

**Nota:** Como sabemos que os gustan las normas y las cosas claras, a la hora de trabajar con distintos tipos de comillas, la opción recomendable es usar un único tipo a lo largo de todo el código de tu programa y usar `\` para "escapar" (convertir a un carácter normal) las comillas anidadas (ej: `'What\'s up!'`).

Ejemplos de `string`s válidos en JavaScript:

```js
"a"                                   // Devuelve "a"
'b'                                   // Devuelve "b"
"Hola"                                // Devuelve "Hola"
'¿Qué tal?   '                        // Devuelve "¿Qué tal?   " (nótese los espacios)
"%^%&^%Ω"                             // Devuelve "%^%&^%Ω"
"Lorem ipsum dolor"                   // Devuelve "Lorem ipsum dolor"
"123123"                              // Devuelve "123123"
'"Lorem ipsum dolor sit amet..."'     // Devuelve ""Lorem ipsum dolor sit amet...""
"\"Lorem ipsum dolor sit amet...\""   // Devuelve ""Lorem ipsum dolor sit amet...""
'It\'s ok'                            // Devuelve "It's ok"
```

#### Concatenando cadenas

Podemos unir varias cadenas en una usando el operador `+`.

```js
const morningGreeting = 'Buenos días';
const adalaber = 'Adalaber';

const morningAdalaberGreeting = morningGreeting + ' ' + adalaber + '.';

console.log('morningAdalaberGreeting: ', morningAdalaberGreeting);
```

<!-- @TODO: add exercise 6-->

En casos un poco más elaborados la concatenación hace que el código sea difícil de leer y por lo tanto de manejar. Por suerte esta fue otra de las áreas mejoradas en la última versión de JavaScript (ES6). Vamos a verlo en el siguiente bloque.

#### Interpolación de cadenas (Template strings)

 Nos facilita insertar variables y operaciones dentro de cadenas de texto. Para eso escribiremos las cadenas entre acentos graves o _backticks_ (`` `This is a string` ``), en vez de entre comillas, y las expresiones o variables entre `${` y `}` (`${expressionOrVariable}`).

```js
const name = 'Ada';
const surname = 'Lovelace';

console.log(`My name is ${name} ${surname}.`):
// 'My name is Ada Lovelace.'
```

También podemos evaluar operaciones directamente:

```js
const firstItemPrice = 5;
const secondItemPrice = 3;

console.log(`Total amount: ${firstItemPrice + secondItemPrice}€`);
// Total amount: 8€
```

La interpolación de cadenas también nos permite escribir cadenas de varias líneas sin escapar los saltos de línea, como era necesario en ES5:

```js
const element = document.querySelector('#element');
const textToShow = 'Hey, this is important.';

// ES5
element.innerHTML = '\
<div class="popup">\
  <span>' + textToShow + '</span>\
</div>';

// ES6
element.innerHTML = `
<div class="popup">
  <span>${textToShow}</span>
</div>`;
```

[&blacktriangleright; Interpolación de cadenas en Codepen][codepen-string-interpolation]

* * *

#### EJERCICIO 7

El objetivo de este ejercicio es pintar tres elementos dentro de una lista. Cada uno de ellos contendrá una imagen. Las imágenes y textos los obtendremos a partir de los siguientes datos:

```js
const firstDogImage = 'https://dog.ceo/api/img/schipperke/n02104365_8156.jpg';
const firstDogName: 'Dina';

const secondDogImage = 'https://dog.ceo/api/img/collie-border/n02106166_355.jpg';
const secondDogName: 'Bobby';

const thirdDogImage = 'https://dog.ceo/api/img/schipperke/n02104365_8156.jpg';
const thirdDogName: 'Lana';
```
En este caso para añadir cada uno de los elementos utilizaremos la propiedad `innerHTML` y la interpolación de cadenas.

* * *

#### Longitud de string

Toda cadena en JavaScript tiene una longitud, esta se puede consultar mediante la propiedad `length`.

```js
const browserName = 'Mozilla';

console.log('Mozilla is ' + browserName.length + ' code units long');
```

* * * 
### EJERCICIO 8

Con todo lo aprendido hasta ahora vamos a hacer un programa que pinte en HTML lo siguiente:
`El nombre de mi compañera es Leticia Fernández Sánchez, y está compuesto por 23 caracteres`.

* * *


### Cadenas de números

Es importante saber que cualquier número entre comillas, como por ejemplo `"232"`, será considerado como texto (string). Por tanto tenemos que estar atentos a las comillas para saber diferenciar entre uno y otro.

De la misma manera, siempre que recojamos contenido de HTML, por ejemplo con `innerHTML`, el valor será de tipo string. `parseInt()` función muy útil que convierte una cadena en un numero, es decir, parsea un string en un número entero.

* * *
#### EJERCICIO 7

Vamos a duplicar el ejercicio 5 y a modificarlo, recogiendo la edad con la que vamos a operar de una etiqueta que prepararemos en HTML.
* * *

* * *
#### EJERCICIO 8

Copia y pega en la consola la siguiente operación:

```js
2 + 3 + '5'
```

Ahora realiza lo mismo con esta otra:

```js
'2' + 3 + 5
```

Compara y comenta los resultado con tu compañera.


* * *

## Resumen

Con esto hemos iniciado nuestro viaje en el mundo de la programación y hemos empezado a aprender las bases, pero ya podemos crear pequeños programas que tienen utilidad, y se muestran en el navegador, todo en un par de días con este lenguaje de programación.


### Recursos
<!--
@TODO: 
-->
