# Buenas prácticas en React

## Contenidos

<!-- TOC -->

- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)
- [EJERCICIO 3](#ejercicio-3)

<!-- /TOC -->

## Introducción

Hemos visto ya las funcionalidades más básicas de la librería. En esta sesión nos centraremos en repasar lo ya visto e introducir buenas prácticas en el uso de React.

## ¿Para qué sirve lo que vamos a ver en esta sesión?

Para poder escribir un código de React más legible y usando el "React way", es decir, haciéndolo de la forma en que lo hacen los desarrolladores de React.

## Uso de expresiones y programación funcional

Como ya sabemos, en React podemos mezclar código de JSX (nuestro HTML en JS) y código JavaScript metiéndolo entre llaves `{ }`. Pero el código que metemos entre llaves debe ser una expresión, es decir, un trozo de código que devuelve un resultado. Por eso, por ejemplo, no podemos meter código con `if`/`else` o hacer un `for` en JSX. Si necesitamos hacerlo, debemos llevarnos ese código a una nueva función (o método) y ejecutarla entre las llaves `{miFucn()}` ya que ejecutar una función sí es una expresión.

Debido a esto, el código de React que escriben los desarrolladores tiende a constar de expresiones y usar patrones como en encadenamiento (_chaining_), por ejemplo, usando métodos funcionales de array para manejar listados en lugar de bucles. El encadenamiento consiste en operar sobre el resultado de una expresión encadenando otra acción mediante el operador punto `.`. Vamos a ver un ejemplo de esto que ya lo hemos estado usando:

```js
const numbers = [1, 4, 6, 8, 45, 89];

const incrementedAndEvenNumbers = numbers
  .map(n => n + 1)
  .filter(n => n % 2 === 0);
```

En este ejemplo, partimos de un conjunto de números, sobre los que queremos realizar 2 operaciones:

- incrementarlos en 1
- filtrar los pares
  Hemos realizado ambas operaciones encadenando un `map` que añade 1 a cada número con un `filter` para quedarnos solo con los números pares resultado de la operación anterior.

---

#### EJERCICIO 1

**Numeritos**

Vamos a crear una aplicación de React que, dado un listado de números como el del ejemplo anterior, los pinta en pantalla (usaremos un `ul` y sus `li`s ¡por supuesto!). Para pintarlos vamos a usar la función `.map` para pasar de un listado de números a un listado de elementos de JSX.

a) Vamos a añadir un formulario a la página, que contiene un input donde podemos introducir un número. Si ponemos, por ejemplo un 6, se mostrarán en pantalla solo los números mayores de 6. Usaremos `filter` y el patrón _chaining_ para conseguirlo.

b) Vamos a añadir un nuevo campo al formulario de tipo checkbox, que al marcarlo filtre además los números pares, desapareciendo de pantalla los impares. Este filtro debe actuar además del anterior, es decir, podremos filtrar los números mayores de 6 y que además sean pares.

---

## Pintado condicional

Otro de los patrones de uso de React es el _conditional rendering_ o pintado condicional. Usando expresiones (como hemos hablado antes) vamos a poder pintar en pantalla unos elementos u otros.

### Ternarios

Podemos usar los ternarios en lugar de los `if`/`else` para pintar algo en pantalla dependiendo, por ejemplo, del estado ya que los ternarios sí son expresiones.

```js
const { isEditMode } = this.state;

return isEditMode ? (
  <p>Editing mode is ON ...</p>
) : (
  <p>Editing mode is OFF ...</p>
);
```

Esto suele usarse mucho para mostrar elementos de _loading_ (_loaders_) mientras, por ejemplo, se carga información del servidor.

### Comprobaciones y valores por defecto

Muchas veces vamos a querer hacer comprobaciones antes de pintar cosas en pantalla, por ejemplo, que una variable o sus claves no sean nulas. Lo haremos usando el operador `&&` ya que las condiciones se ejecutan en orden desde la primera y si alguna es falsa dejan de ejecutarse. Por ejemplo, aquí comprobamos primero que `data` no sea null, luego que tenga una clave `name` que no sea nula y si ambas se cumplen pinta el contenido en pantalla. Si no se cumplen, no se pintará nada.

```js
return data && data.name && <p>Bienvenido, {data.name}</p>;
```

También se usa bastante el operador `||` que ya hemos visto sirve, por ejemplo, para dar valores por defecto. Esto es porque la segunda parte del las operaciones solo se ejecuta si la primera es falsa (o null que es un falsy).

```js
return data && <p>Bienvenido, {data.name || 'invitado'}</p>;
```

En este ejemplo dejamos la primera comprobación de que `data` no sea null, y luego si el nombre no está definido usamos el valor de `'invitado'`.

### `null` no pinta nada

Para terminar estos ejemplos sencillo de pintado condicional, debemos saber que si una expresión dentro de JSX devuelve `null` no se pintará nada en pantalla.

```js
const { quixoteFan } = this.state;

return quixoteFan ? <p>En un lugar de La Mancha ...</p> : null;
```

---

#### EJERCICIO 2

**Colapsables**

Vamos a partir de nuestro ya [querido JSON con un listado de paletas](https://raw.githubusercontent.com/Adalab/Easley-ejercicios-de-fin-de-semana/master/data/palettes.json), para pintar un listado de colapsables. Vamos a pintar el nombre de la paleta y la flechita del colapsable por cada una. Al desplegar un colapsable, se muestra su contenido, que es simplemente el campo `from` del JSON.

> NOTA: Recordad que debemos guardar en el estado del componente de React si los colapsables están o no desplegados. Es más sencillo si solo se puede tener un colapsable desplegado a la vez.

---

## Listados y keys

Cuando manejamos listados de datos en React, normalmente convertimos estos arrays en arrays de elementos JSX para poder pintarlos. Para ayudar a que la librería de React tenga mejor rendimiento, es importante indicar un atributo `key` que sea único en los listado de componentes JSX. De hecho, seguramente ya te habrás topado con errores en la consola que React advierte por este motivo.

Para solucionarlo, debemos indicar un atributo `key` que sea único en ese array (no en la página).

```js
const fruits = ['orange', 'pear', 'apple'];

return (
  <ul>
    {fruits.map(fruit => (
      <li key={fruit}>{fruit}</li>
    ))}
  </ul>
);
```

Cuando no tenemos un identificador único, como último recurso podemos hacer uso del índice del elemento dentro del array.

```js
const fruits = ['orange', 'pear', 'apple', 'orange];

return (
  <ul>
    {fruits.map((fruit, index) => (
      <li key={index}>{fruit}</li>
    ))}
  </ul>
);
```

#### EJERCICIO 3

**Keys or not keys**

a) Para terminar, vamos a repasar los ejercicios anteriores y comprobar que no tenemos errores en la consola debidos a la ausencia de keys.

b) En el ejercicio anterior vamos a extraer un nuevo componente llamado `ColapsiblePalette`. ¿Dónde hay que poner el `key` ahora?

---

## Recursos externos

- [Conditional Rendering](https://reactjs.org/docs/conditional-rendering.html)
- [Lists and keys](https://reactjs.org/docs/lists-and-keys.html)
