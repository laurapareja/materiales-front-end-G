# Introducción a la programación 2

## La consola de JavaScript

En las herramientas para desarrolladores de Chrome (las DevTools) la segunda pestaña es una consola JavaScript. Una consola nos permite escribir instrucciones JavaScript que al dar al Enter se ejecutan. En la consola puedes probar a hacer sumas, declarar variables, funciones, etc.

Con la consola también podemos interactuar desde nuestro programa JavaScript, es decir, desde el código que escribimos en nuestro fichero `.js`. Una de las cosas que podemos hacer es escribir datos que comúnmente se denomina *loguear* datos. Lo hacemos mediantes una función `console.log()` en la que lo que pongamos entre paréntesis será lo que se escriba en la consola. A priori puede parecer que esto no tiene mucha utilidad ya que en nuestra página web no veremos nada, solo si abrimos las herramientas de desarrolladores. Pero con el tiempo le irás comprobando lo útil que es, por ejemplo, para depurar (resolver) errores en el código.

```js
console.log('Hola');

var num = 56;
console.log(num);
```

> Prueba a abrir la consola y escribe instrucciones para que veas cómo puedes ejercutar JS. También prueba a escribir datos en la consola desde tu programa con `console.log`

## Tipos de datos

En la sesión anterior hablado de que programar es básicamente realizar operaciones sobre datos para obtener un resultado concreto. Bien, esos datos con los que trabajamos en nuestro código se representan mediante valores. Por tanto un valor no es más que la representación de un dato sobre la que podemos aplicar las reglas comentadas anteriormente. Si queremos mostrar la temperatura en una pantalla, necesitaremos el valor numérico (por ejemplo, 27) que represente el dato de esa temperatura y sobre ese valor aplicaremos las reglas para obtener el resultado deseado (sacar la media de temperatura, calcular el día que más calor ha hecho, etc.).

Se aprecia con esto que la base de la información de nuestra aplicación reside en los valores. Éstos serán los encargados de representar los datos y serán sobre los que apliquemos las operaciones necesarias.

En JavaScript existen por defecto seis tipos distintos de datos, todos ellos los veremos a lo largo del curso, pero por el momento vamos a centrarnos en dos: `number` (número) y `string` (cadena de caracteres).

Cada uno de ellos, según sus características, se utilizará para representar un tipo de valor concreto. El tipo `number`, como habrás podido deducir, se utilizará para representar números, mientras que el tipo `string` se utilizará para representar texto. Este segundo se llama `string` porque está compuesto de varios caracteres (letras) que unidos entre sí forman una cadena (string).

### String

_String_ traducido al español significa cadena y como su nombre indica es el tipo de valor utilizado para representar cadenas de caracteres, que viene a ser básicamente texto. Cualquier tipo de texto, ya sean caracteres sueltos ("a", "b", "0") o en conjunto ("hola", "las 13:40", "2312312") estará incluido dentro de este tipo de valor.

En los ejercicios anteriores, siempre que hemos escrito entre comillas (`''`) un texto, lo que hemos hecho es incluir en el código un _string_, decirle al programa encargado de ejecutar nuestro código que eso es un texto y que debe utilizarlo como tal en vez de entenderlo como una orden (como hace con `alert`).

Para representar un string en JavaScript, como se comenta en la sección anterior, se puede utilizar tanto texto envuelto entre comillas simples (`''`) como dobles (`""`). Ambas son totalmente válidas y funcionan de la misma manera salvo que las comillas simples no pueden contener dentro otras comillas simples y las dobles no pueden contener dobles. De esta forma, `'Esto es un 'bug''` da error porque el navegador al ejecutar el código entiende que un texto termina antes de `bug` y comienza otro texto después de `bug`. Pasaría lo mismo si usamos `"Esto es un "bug""`.

Para evitar estos errores producidos por el uso de comillas anidadas existen dos soluciones:
- Usar comillas simples siempre que el texto contenga comillas dobles o viceversa
- Usar la barra inclinada (`\`) delante de las comillas anidadas (Ej: `'I\'m a front-end developer'`). De esta forma decimos a JavaScript que esas comillas son texto normal y no van a ser usadas para marcar el final del string y por tanto no se produce el error.

**Nota:** Como sabemos que os gustan las normas y las cosas claras, a la hora de trabajar con distintos tipos de comillas, la opción recomendable es usar un único tipo a lo largo de todo el código de tu programa y usar `\` para "escapar" (convertir a un caracter normal) las comillas anidadas (ej: `'What\'s up!'`).

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

### Number

Cómo su nombre indica, el tipo de valor _number_ comprende cualquier tipo de número utilizado en JavaScript. Hay varios subtipos de números en JavaScript pero de momento aprenderemos los más importantes, números enteros o _integers_ y números decimales o _floating point numbers_.

En JavaScript los números enteros se representan directamente con cifras, por lo que es totalmente válido escribir `14232` o `-42` en nuestro código. Por otro lado, los números decimales se escriben igual que en inglés, es decir, utilizando puntos en vez de comas. Por ejemplo, podemos representar el número _1,32_ escribiendo `1.32`.

Las anteriores son las únicas reglas gramaticales a la hora de escribir números enteros y decimales. Pero escribir números sin hacer nada con ellos no tiene ninguna utilidad, lo que queremos es poder obtener otros números, es decir, poder operar con ellos. Esto lo podemos conseguir mediante los operadores de suma, resta, multiplicación, división y módulo.

Es importante saber que cualquier número entre comillas, como por ejemplo `"232"`, será considerado como texto (string). Por tanto tenemos que estar atentos a las comillas para saber diferenciar entre uno y otro.

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

### Módulo

El operador de resto (`%`), también llamado operador de módulo (_module_), es un operador especial utilizado en JavaScript para obtener el resto de la división entre dos valores. Si escribimos `5 % 2` en nuestro código, este nos devolverá el resto de esa operación, 1.

```js
0 % 80 // Devuelve 0
4 % 5  // Devuelve 4
13 % 5 // Devuelve 3
9 % 3  // Devuelve 0
```

El operador de módulo tiene el mismo orden de ejecución que los operadores de multiplicación y división.

## Booleanos

Los booleanos son tipos de datos de JavaScript que guardan información del tipo verdadero o falso. Solo pueden tener los valores `true` o `false`. Por ejemplo:
```js
var filled = false; //Este booleano es falso

var solved = true; //Este booleano es verdadero

## El código como una caja negra

JavaScript, al igual que otros lenguajes de programación, ejecuta el código de manera similar a una caja negra. Todas las operaciones se ejecutan pero si no indicamos de forma explícita que muestre algo (como cuando lo hacemos con el `alert`) no se mostrará nada en la pantalla y será como si ese código no se hubiera ejecutado, aunque lo haya hecho.

Podéis probar esto escribiendo el siguiente código en un archivo de JavaScript, enlazandolo a un archivo HTML y abriendo ese HTML en un navegador:

```js
10 + 10 + 10;
240 / 3;
4 * 8 - 12;
```

Al escribir este código y ejecutarlo en nuestro navegador, será como si no hubiésemos hecho nada pero, en realidad, este se habrá ejecutado sin que se perciba o eso nos han contado, porque no podemos saberlo :).

Debido a este comportamiento, vamos a utilizar por el momento `alert` para ver el resultado de las operaciones en una ventana de alerta. Si lo hacemos con el anterior ejemplo, podremos ver el resultado de las operaciones:

```js
alert(10 + 10 + 10); // Muestra 30 en la ventana de alerta
```

En el futuro veremos cómo mostrar este código directamente en la página sin que tenga que aparecer la ventana, pero de momento trabajaremos así para no añadir demasiada complejidad al proceso de aprendizaje.


* * *
#### EJERCICIO 3

El precio de la fruta

Imagina que vamos a la frutería y compramos lo siguiente:

- 2 kilos de kiwis a 5€/kg
- 3 kilos de peras conferencia (no una cualquiera) a 2€/kg
- medio kilo de uvas a 4€/kg

Con lo que hemos visto durante los ejemplos y textos anteriores y usando JavaScript, vamos a calcular el precio total como si lo hiciesemos en una hoja de toda la vida pero de manera mucho más guay. El resultado debe mostrarse en una ventana de alerta.

* * *
#### EJERCICIO 4

¡Págame, tía!

Nos vamos de cena de Navidad, ¡qué alegría! Somos en total 9 personas y la cuenta del restaurante japonés es de 128€. Ana tiene que pagar 2€ más que los demás porque ha pedido un chupito de sake. ¿Cuánto tenemos que pagar cada una? ¿Y Ana? Hagamos un pequeño programa en JavaScript para calcularlo.

* * *
#### EJERCICIO 5

Calcular cuál va a ser el siguiente año bisiesto

Vamos a escribir un pequeño programa que nos permita saber cuál será el siguiente año bisiesto. Para aportar un poco de información, sabemos que los años bisiestos se producen cada cuatro años a partir del año 0. El primer año bisiesto fue 4, el segundo 8 y así progresivamente. La idea de este ejercicio es que, si estuviésemos en el año 3, al ejecutarlo apareciese una ventana de alerta con el texto "4", ya que el año 4 sería el siguiente año bisiesto.

**Nota:** En este caso tenemos que escribir nosotros el año en el que estamos para saber cuando será el siguiente año bisiesto pero en los siguientes párrafos veremos cómo introducir un dato desde el navegador para poder utilizarlo desde nuestro código. Esto nos permitirá hacer un programa más lógico, porque podremos mostrar cuál será el siguiente año bisiesto a partir del año que hemos introducido.

* * *
#### EJERCICIO 6

Calcular el número total de horas que hemos vivido

En este caso vamos a crear un código que nos diga cuantas horas en total hemos vivido. Por ejemplo, si alguien tiene 60 años, este código debería de mostrar un mensaje con el número "525600".

**Nota:** En este caso no tendremos en cuenta los años bisiestos para no complicar mucho el ejercicio.
* * *
