# Funciones

<!-- TOC depthFrom:4 depthTo:4 insertAnchor:false updateOnSave:true -->

- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)
- [EJERCICIO 3](#ejercicio-3)
- [EJERCICIO 4](#ejercicio-4)
- [EJERCICIO 5](#ejercicio-5)
- [EJERCICIO BONUS 1](#ejercicio-bonus-1)

<!-- /TOC -->




## Funciones

Una función es un bloque de código que definimos una vez y lo reutilizamos las veces que queramos; un conjunto de instrucciones a las que podemos pasar diferentes datos para que nos devuelva resultados distintos.

Durante esta sesión veremos cuáles son las principales características de este recurso de programación y cómo utilizarlo en nuestro código para sacarle el máximo partido.


## ¿Para qué sirve lo que vamos a ver en esta sesión?

Las funciones son muy útiles a la hora de crear un código único para usarlo en distintas partes de nuestro programa. El beneficio de esto es que si en el futuro queremos modificar algo de ese código lo haremos en un único sitio aunque se utilice en decenas de sitios diferentes. Las funciones se ejecutan en distintos momentos y con distintas características gracias a los _parámetros_.

Otra de las ventajas de las funciones es que devuelven un valor, es decir, realizan una operación y pueden devolver un dato. Ese dato podemos asignárselo a una variable o usarlo dentro de otra operación. O incluso podemos prescindir de él si no nos interesa para nada.

Las funciones son una forma de agrupar código que vamos a usar varias veces permitiéndonos además, pasar diferentes valores para obtener diferentes resultados.

Podemos intentar hacer un paralelismo con el café, más o menos todo el mundo sabe hacer un café, desde los ingredientes a los diferentes pasos. Y cada vez que queramos uno seguimos todos los pasos uno a uno, y al final tendremos un café.

Ahora, las funciones serían como estas cafeteras modernas, a las que dependiendo de la cápsula que uses te hace un café diferente. Cuando activo la cafetera (llamo a la función) detecta qué tipo de capsula he introducido (parámetros) y me hace (me devuelve) un café u otro:
- Si utilizo una de estas cápsulas de hipster purista tendré un café de esos que no te dejan tomar si no llevas camisas de cuadros, patinetes y unas gafas de pasta.
- Si utilizo una cápsula más divertida que añada espuma, caramelo y coco pues tendré que huir de los hispters de antes porque para ellos este tipo de café debería ser ilegal.

Un ejemplo de esto sería:

```javascript
function makeMeCoffe( coffeName ) {
  return `Aquí tiene su ${coffeName}, que lo disfrute`;
}
```

De manera que podemos llamar varias veces a la función y obtener "cafés" diferentes:
```javascript
makeMeCoffe( 'Café hipster con cuerpo de minotauro y esencia de madera y oro' );
// devuelve "Aquí tiene su Café hipster con cuerpo de minotauro y esencia de madera y oro, que lo disfrute"

makeMeCoffe( 'Café con coco, nata y un toque de menta' );
// devuelve "Aquí tiene su Café con coco, nata y un toque de menta, que lo disfrute"

```

## ¿En qué casos se utiliza?
Por ejemplo, en los siguientes casos:
- Si tenemos un código que convierte la primera letra de un texto a mayúsculas y vamos a usar ese código en varias partes de nuestro programa, creamos una función y ejecutamos la función en cada uno de los sitios necesarios
- Si queremos añadir varias clases a diferentes elementos HTML en función de la medida de la página web podemos crear una función y utilizarla en cada uno de ellos
- Si queremos enviar datos a un servidor, la mayoría de las veces es muy parecido y sólo cambian unos datos. Podríamos hacer una función y reutilizarla y usar distintos datos en cada una mediante los parámetros de la función (que veremos durante esta sesión)


## Declaración y uso de funciones
Para utilizar una función debemos declararla en algún sitio de nuestro código.

La estructura para declarar una función es
- primero la palabra reservada `function` seguida del nombre de la función
- después entre paréntesis `( )` los parámetros de la función separados por comas `,` y que si no tiene parámetros estará vacío
- un bloque de código entre llaves `{ }` con las instrucciones de código de la función

```javascript
//Función sin parámetros
function hi() {
	return 'Hola';
}

//Función con parámetros
function sum(a, b) {
	return a + b;
}
```

Si añadimos las declaraciones anteriores de funciones a nuestra página, no veremos ningún efecto. Esto es porque solo estamos declarando las funciones, es decir, diciendo que existen pero nada más.

Para utilizar (también se le puede llamar *ejecutar* o *invocar*) una función simplemente usamos el nombre de la función seguida de paréntesis donde pasaremos los parámetros o argumentos separados por comas `,`.

```javascript
console.log( hi() );
//Muestra en la consola la palabra 'Hola'

console.log( sum(1, 4) );
//Muestra en la consola un 5
```
>NOTA: Esta sintaxis para utilizar funciones te suena, ¿verdad? Hasta ahora hemos estado ejecutando algunas funciones ya declaradas en el navegador como `querySelector('.title')` a la que le pasamos por parámetro una cadena con el selector que buscamos y nos devuelve la referencia a dicho elemento en nuestro HTML.

Se pueden crear funciones sin nombre, estas funciones se llaman _funciones anónimas_. Estas funciones se suelen emplear para cosas que veremos en el curso más adelante, como asignarlas a una propiedad de un objeto o pasarlas como un callback. Un ejemplos de función anónima:

```javascript
const sum = function(a, b) {
	return a + b;
};

// La llamamos con el nombre de la variable
sum(2,3); // devuelve 5
```

## Parámetros y valores de retorno

Los *parámetros* son los datos que definimos en una función y que, a la hora de ejecutarla, serán sustituidos por los *argumentos* que le pasemos. Por tanto, en la declaración de la función le llamamos parámetros y en la ejecución le llamamos argumentos. Las funciones pueden tener 0, 1 o más parámetros separados por comas `,`.

Una función puede devolver un valor utilizando la palabra clave `return` seguida del valor que queremos devolver. Para devolver una variable `result`, utilizaremos `return result;` en el código.

```javascript
function sum(a, b) {
	const result = a + b;

	return result;
}

const sumResult = sum(3, 4); //sumResult vale 7
```

Por defecto, si en una función no indicamos un valor de retorno usando `return`, la función devolverá el valor `undefined`. El valor _undefined_ en JavaScript indica que una variable ha sido declarada pero no posee ningún valor, en este caso determina que la función no tiene asignado ningún valor de retorno y por eso devuelve `undefined`.

Cuando ejecutamos una instrucción `return` dentro de una función, termina la ejecución de la función. Todo el código que se fuese a ejecutar después de ese `return` será ignorado, como si no existiese. Por tanto, debemos evitar escribir líneas de código después de un `return` y normalmente será la útlima línea de código de una función.

* * *
#### EJERCICIO 1

**Función multiplicación**

Crea una función que reciba como argumento dos valores y devuelva como valor de retorno la multiplicación de ambos. Haz tres pruebas con distintos números para comprobar que funciona correctamente y muestra el resultado en la consola usando `console.log()`.

* * *
#### EJERCICIO 2

**Función media**

Crea una función que reciba 4 parámetros, cada uno con un número, y devuelva como valor la media de todos ellos. Haz tres pruebas con distintos números para comprobar que funciona correctamente y muestra el resultado en la consola.

* * *

#### EJERCICIO 3

**Ticket con IVA**

Crea una función que reciba como parámetro un número, que representará un precio, y devuelva un texto en el que ponga el precio sin IVA, el IVA (21%) y el total. Por ejemplo, si pasamos por parámetro un 10, la función pintará en la consola `"Precio sin IVA: 10, IVA: 2,1 y Total: 12,1"`.

Para probar que funciona, ejecuta la función recogiendo el resultado en una variable e imprímela en la consola para comprobarlo.

* * *

## Ámbito de las variables

Una variable creada dentro del cuerpo de una función sólo será accesible desde dentro de esa función.

A esto se le llama ámbito (en inglés, _scope_) y permite que no se generen conflictos entre funciones con variables que tienen un nombre idéntico.

Desde dentro de una función podemos utilizar las variables que se hayan definido fuera de cualquier función.

Por ejemplo:

Comprueba cuál será el resultado de las siguiente operaciones:

```javascript
// Usamos una variable de ámbito global

const secretLetter = 'y';
function mySecretLetter() {
  return secretLetter;
}
console.log( mySecretLetter() ); // devuelve "y"
console.log( secretLetter ); // devuelve "y"
```

```javascript
// modificamos una variable de ámbito global
let secretLetter = 'y';
function mySecretLetter() {
  secretLetter = 'x';
  return secretLetter;
}
console.log( mySecretLetter() ); // devuelve "x"
console.log( secretLetter ); // devuelve "x"
```

```javascript
// Usamos una variable de ámbito local que se llama igual que la global
const secretLetter = 'y';
function mySecretLetter() {
  const secretLetter = 'x';
  return secretLetter;
}
console.log( mySecretLetter() ); // devuelve "x"
console.log( secretLetter ); // devuelve "y"
```

```javascript
// intentamos usar una variable local fuera de su ámbito
function mySecretLetter() {
  const secretLetter = 'x';
  return secretLetter;
}
console.log( mySecretLetter() ); // devuelve "x"
console.log(secretLetter); // devuelve undefined porque esta variable solo existe dentro del ámbito de la función
```


## Arrow functions

Las arrow functions ("funciones flecha") de ES6 son una forma simplificada para declarar funciones anónimas. La sintaxis básica es la siguiente:

```javascript
const sum = (a,b) => {
  return a + b;
};

// y la ejecutamos usando la variable a la que la hemos asignado:
sum(2,3); // devuelve 5;

// Anteriormente vimos esta misma función con la forma "normal"
const sum = function(a,b) {
  return a + b;
};
```

### Paréntesis opcionales
En las funciones flecha podemos evitar los paréntesis solo cuando la función tenga 1 único parámetro:
```javascript
const printWaitingTime = minutes => {
  console.log(`Please, wait ${minutes} minutes`);
};

// equivale a
const printWaitingTime = (minutes) => {
  console.log(`Please, wait ${minutes} minutes`);
};
```

### Llaves y return implícito
Escribir o no las llaves ({}) significa dos cosas distintas. Solo podremos no escribirlas cuando la función tenga una sola sentencia; es decir, cuando se ejecute una sola orden dentro (un console.log(), un cambio en un elemento HTML, un incremento en un contador, etc.). Cuando no escribimos las llaves, el valor que devuelve esa sentencia será el return de la función. Eso nos permite escribir en menos líneas funciones muy sencillas:

```javascript
const printWaitingTime = minutes => `Please, wait ${minutes} minutes`;
console.log( printWaitingTime(4) );
// devuelve "Please, wait 4 minutes"
};

// equivale a
const printWaitingTime = (minutes) => {
  return `Please, wait ${minutes} minutes`;
};
console.log( printWaitingTime(4) );
// devuelve "Please, wait 4 minutes"
```

#### EJERCICIO 4

**Calculador de modelo de caja**

Como hemos visto en las clases anteriores, en CSS tenemos dos tipos de cálculo para las dimensiones de un elemento: `border-box` y `content-box`. Vamos a realizar un calculador al que le pasaremos 4 parámetros y nos devolverá el ancho del contenido, en caso de ser _border-box_ o el ancho total de la caja, en caso de ser _content-box_.

La función tendrá 4 parametros: el primero será un booleano para especificar si es border-box o no, el segundo será el ancho del contenido o de la caja entera, el tercero el padding y el cuarto el borde.

Para probar que funciona, ejecuta la función recogiendo el resultado en una variable e imprímela en la consola para comprobarlo.

* * *

#### EJERCICIO 5

**Arrow functions everywhere**

Vamos a rehacer alguno de los ejercicios anteriores con funciones flecha. ¡A lo loco!

* * *

## Bonus: Funciones en todas partes

Se pueden ejecutar funciones dentro de otras funciones.

Se pueden pasar funciones como argumentos para otras funciones, devolver funciones como valores de otras funciones y guardar funciones en variables.

## Recursos externos

### Curso de Ada Lovelace en Youtube

Este curso explica bastante bien y de forma breve qué son las funciones y como trabajar con ellas.

- [Funciones. Introducción](https://www.youtube.com/watch?v=PEfw6xuj8Y0&list=PLI7nHlOIIPOJtTDs1HVJABswW-xJcA7_o&index=16)
- [Funciones anónimas](https://www.youtube.com/watch?v=GstPXAffmmI&index=17&list=PLI7nHlOIIPOJtTDs1HVJABswW-xJcA7_o)
- [Funciones. Parámetros y argumentos](https://www.youtube.com/watch?v=5VVBrfWQ2Wk&index=18&list=PLI7nHlOIIPOJtTDs1HVJABswW-xJcA7_o)
- [Ámbito de variables](https://www.youtube.com/watch?v=HlY2jF74s_c&list=PLI7nHlOIIPOJtTDs1HVJABswW-xJcA7_o&index=19)

### Libros Web

Si prefieres un recurso escrito para aprender, aquí tienes la explicación de las funciones y el ámbito de las variables en JavaScript de la mano del libro de Introducción a JavaScript por Libros Web.

- [Funciones](http://librosweb.es/libro/javascript/capitulo_4/funciones.html)
- [Ámbito de las variables](http://librosweb.es/libro/javascript/capitulo_4/ambito_de_las_variables.html)
