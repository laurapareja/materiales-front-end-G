# Array y bucles 2

<!-- TOC depthFrom:4 depthTo:4 -->

- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)
- [EJERCICIO 3](#ejercicio-3)
- [EJERCICIO 4](#ejercicio-4)
- [EJERCICIO 5](#ejercicio-5)
- [EJERCICIO 6 BONUS](#ejercicio-6-bonus)
- [EJERCICIO 7 BONUS](#ejercicio-7-bonus)
- [EJERCICIO 8 BONUS](#ejercicio-8-bonus)

<!-- /TOC -->

## Introducción

En esta sesión vamos a seguir profundizando en el uso de arrays para manejar listados de datos. Aprenderemos métodos de array muy útiles que nos proporciona el lenguaje Javacript para poder almacenar nueva información en un array y procesar los datos que contiene.


## Métodos de array

A continuación veremos algunos de los métodos básicos que más se utilizan para trabajar con arrays.

### `push`

El método `push()` sirve para agregar uno o más elementos al final de un array. Es una forma común en JavaScript de añadir elementos a un array. Este método tras agregar los elementos al array devuelve la nueva longitud de éste.

```js
const arr = [1, 2, 3];
const newLength = arr.push(3, 5, 6, 7);

console.log(newLength); // Loguea 7, la nueva longitud de arr
console.log(arr); // Loguea 1,2,3,3,5,6,7
```

> **NOTA:** Pocas veces es necesario guardar el resultado del método `push()` en una variable ya que podremos acceder a este valor cuando queramos usando la propiedad `length`. Nosotros normalmente no guardaremos ese valor en una variable, pero es bueno que sepamos cómo funciona exactamente el método.

Como podemos ver, para agregar elementos, pasaremos estos como argumentos del método. Podemos pasar todos los argumentos que queramos sin problema:

```js
var arr = [1, 2, 3];
arr.push(3, 5, 6, 7, 23, 34, 35, 34, 54, 34, 3434, 34); // Esto es totalmente válido
```

---

#### EJERCICIO 1

**Numeritos**

Vamos a crear una función `get100Numbers` que devuelve un array con los números del 1 al 100. Como no nos apetece tener que escribir 100 números a mano, usaremos un bucle y el método `push` para ir guardándolos. Para comprobar que los tenemos todos, vamos a ejecutar la función y loguearlos (con `console.log`) uno a uno en la consola en orden.

---

### `reverse`

El método `reverse()` invierte el orden de un array. El primer elemento pasará a colocarse en la última posición, el segundo pasará a colocarse en la penúltima y así sucesivamente. Este método modifica directamente el array sobre el que se ha utilizado y devuelve ese array actualizado.

```js
const arr = [1, 2, 3];
console.log(arr.reverse()); // Loguea 3,2,1
console.log(arr); // Loguea también 3,2,1 porque reverse modifica arr
```

---

#### EJERCICIO 2

**Sotiremun**

Vamos a crear una nueva función `getReversed100Numbers` que llama a la función del ejercicio anterior para obtener 100 números y los cambia de orden. Para comprobar que los tenemos todos, vamos a ejecutar la función y a loguearlos (con `console.log`) uno a uno en la consola en orden.

---

### `concat`

Este método se utiliza para obtener, a partir de dos o más arrays, uno que combine a todos ellos. Este método no modifica ninguno de los arrays que utiliza para combinarlos, sino que devuelve un **array nuevo**. Para concatenar varios arrays con el método `concat()` lo haremos de la siguiente manera:

```js
const letters = ['a', 'b', 'c'];
const numbers = [1, 2, 3];
const booleans = [true, false];

const result = letters.concat(numbers, booleans);

// result tendrá ['a', 'b', 'c', 1, 2, 3, true, false]
```

El array resultante tendrá los elementos ordenados según el orden en que hemos concatenado los arrays, como se puede observar en el ejemplo.

Puedes consultar el [listado completo de propiedades y métodos de array en MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array).

---

#### EJERCICIO 3

**The numbers**

```js
const lostNumbers = [4, 8, 15, 16, 23, 42];
```

Vamos a crear una función `bestLostNomber` que nos devuelve algunos números del array de [los números de la serie Lost](https://lostpedia.fandom.com/wiki/The_Numbers) que tenemos arriba. La función, debe seguir estos pasos:

1. Crear un nuevo array que contiene solo los números pares que hay en `lostNumbers`. Para conseguirlo vamos a crear un nuevo array vacío y recorrer el array `lostNumbers` para al encontrar un número par, meterlo en el nuevo array.
2. Crear un nuevo array que contiene solo los númper múltiplos de 3 que hay en `lostNumbers`, de una forma similar al anterior.
3. Devolver una concatenación de los 2 arrays anteriores, es decir, que tendrá primero los números pares y luego los múltiplos de 3.

Para comprobar que los tenemos todos, vamos a ejecutar la función y a loguearlos (con `console.log`) uno a uno en la consola en orden.

---

## `querySelectorAll`

Como hemos visto en sesiones anteriores, para recoger un elemento de HTML utilizamos el método `querySelector`. Pero ¿y si queremos recoger más de uno, por ejemplo todas las etiquetas que tengan una determinada clase? `querySelectorAll` al rescate.
Este método devuelve una lista de elementos que funciona de manera similar a un array. Podríamos hacer lo siguiente:

```js
// Guardamos una lista de todos los parrafos de la página
const paragraphs = document.querySelectorAll('p');

// Modificamos el primer párrafo
paragraphs[0].innerHTML = 'Soy el primero';

// Muestra el número de parráfos que hay en nuestra web
console.log(paragraphs.length);

// Iteramos sobre todos los párrafos para asignarles a todos una clase
for (let i = 0; i < paragraphs.length; i++) {
  paragraphs[i].classList.add('highlight');
}
```

---

#### EJERCICIO 4

**Botones de alarma**

Vamos a partir de un HTML que tiene 3 botones con el texto ALARMA en un fondo blanco. Vamos a hacer que al pulsar en cualquiera de ellos, el fondo de la pantalla se ponga rojo. Si volvemos a pulsar en cualquiera de ellos, el fondo se pondrá blanco. Y así sucesivamente. Vamos a hacer uso de `querySelectorAll` para evitar repetir mucho código.

---

#### EJERCICIO 5

**REPASO: Mi lista de tareas**

Hemos creado una aplicación para gestionar un listado de tareas: ¡somos gente muy ocupada! Para eso, hemos creado un objeto literal con el listado de tareas y su estado. Nuestra misión es:

1. Mostrar una frase que indique cuántas tareas hay.
2. Pintar todas las tareas en pantalla.
3. Tachar las ya realizadas.
4. Permitir marcar una tarea como 'completa' o 'incompleta'.

Vamos a partir de este array de datos en nuestro fichero JavaScript:

```js
const tasks = [
  { name: 'Recoger setas en el campo', completed: true },
  { name: 'Comprar pilas', completed: true },
  { name: 'Poner una lavadora de blancos', completed: true },
  {
    name: 'Aprender cómo se realizan las peticiones al servidor en JavaScript',
    completed: false,
  },
];
```

Veamos como afrontar un ejercicio de este tipo, dónde tenemos que unir muchos de los conceptos aprendidos hasta ahora, la organización es clave:

a) **Vamos a por una tarea.** Primero vamos a pintar una tarea, solo una, en una lista de HTML. A continuación vamos a preparar una clase que la modifique, de manera que si fuera una tarea completada `completed: true`, el texto aparezca tachado.

b) **Listado de tareas.** ¡Seguimos con nuestras tareas! Ahora vamos a pintar en pantalla todas la tareas que tenemos en el listado, cada una de las tareas completadas debe aparecer tachada.

c) **Vamos a darle dinamismo.** Ahora viene lo bueno: vamos a añadir la lógica necesaria para completar tareas. Para ello vamos a añadir un `input` de tipo `checkbox` al final de cada tarea que nos falte por completar. El checkbox de las tareas completadas debe aparecer marcado (`checked`). Además, cuando el usuario marque la tarea como completada marcando el checkbox, deben suceder varias cosas:

- la tarea debe mostrarse como completada (tachada)
- debemos modificar su estado (propiedad `completed`) en el array `tasks`.

d) **Tareas totales.** No nos podemos olvidar de los detalles. Añadamos por encima del listado de tareas una frase que diga: Tienes _X_ tareas. _Y_ completadas y _Z_ por realizar. Cada vez que una tarea se marque/desmarque deberiamos actualizar esta información.

---

## BONUS

#### EJERCICIO 6 BONUS

**Crea tu árbol de Navidad**

Para que no nos pille el toro esta Navidad, vamos a crear un código que muestre en consola un árbol de navidad con triángulos (▲). Nosotros le diremos la altura y creará un triángulo con un número igual de lineas que la altura que le hemos pasado. Por ejemplo si le pasamos 5, creará este árbol:

```
▲
▲▲
▲▲▲
▲▲▲▲
▲▲▲▲▲
```

---

#### EJERCICIO 7 BONUS

**Mejora tu árbol de Navidad**

Intenta ponerle una estrella y un tronco al árbol para que quede mucho más mono. Sería algo así:

```
★
▲
▲▲
▲▲▲
▲▲▲▲
▲▲▲▲▲
|
```

---

#### EJERCICIO 8 BONUS

**¡Esto es un abeto!**

Intenta cambiar el código para que aparezca el árbol completo.

```
    ★
    ▲
   ▲▲▲
  ▲▲▲▲▲
 ▲▲▲▲▲▲▲
▲▲▲▲▲▲▲▲▲
    |
```

---

### Trabajar con arrays anidados

Algunas estructuras como una array de coordenadas requieren crear arrays dentro de otros arrays, o lo que es lo mismo, arrays anidados. Si pensamos en ese caso concreto de arrays de coordenadas, vemos que tenemos un array y cada elemento posee dos coordenadas que también se pueden mostrar en array. Esto es posible de llevar a cabo en JavaScript y es una práctica común. En este apartado veremos cómo crear arrays anidados, cómo obtener un valor de ellos y cómo modificarlos.

### Crear un array anidado

Partiendo del ejemplo citado anteriormente del array de coordenadas, vamos a declarar un array anidado en JavaScript:

```js
const coordinates = [[4, 3], [9, 2], [2, 6]];
```

Como se puede observar, para crear un array anidado simplemente añadiremos un array dentro de otro. De esta forma podemos crear arrays con varios niveles de anidación pero normalmente se darán pocos casos en los que necesitemos más allá de dos niveles de anidación:

```js
const coordinates = [[[4, 5], [2, 9]], [[1, 4], [4, 6]]];
```

La explicación a esto es que en JavaScript un array puede utilizarse como cualquier otro tipo de dato y por tanto podemos perfectamente meter arrays dentro de otros o incluso combinar arrays anidados con números o strings (aunque no es recomendable).

```js
const randomData = [[4, 5], 'hello', 123123123];
```

### Acceder al valor de un array anidado

Cuando tenemos estructuras de datos anidadas, como en el caso de arrays anidados, lo que se hace para acceder a los valores es algo así como establecer una hoja de ruta, será como decirle al programa _"Del array X quiero el elemento Y y dentro de ese elemento quiero el elemento Z "_. Veamos cómo se traduce esto en código:

```js
const coordinates = [[4, 3], [9, 2], [2, 6]];

const firstcoordinate = coordinates[1]; // De las coordenadas obtenemos el segundo valor ([9,2])
const x = firstcoordinate[0]; // De la primera coordenada obtenemos el primer valor (9)

/*
Ese mismo proceso podemos hacerlo en un paso:
De las coordenadas obtenemos el primer valor y de ese valor obtenemos el primer valor también
*/

const firstElemX = coordinates[1][0]; // firstElemX es igual a 9
```

En el código del ejemplo, si tuviésemos otro nivel más de anidación simplemente tendríamos que añadir otro corchete con el índice del elemento que queremos obtener `deepNestedArr[1][2][1]` y así sucesivamente.

## Modificar elementos anidados

Para modificar elementos, la sintaxis es muy similar a la de acceder al valor de un array anidado:

```js
const coordinates = [[4, 3], [9, 2], [2, 6]];

coordinates[1][0] = 8;
/*
coordinates = [
  [4,3],
  [8,2],
  [2,6]
];
*/
```

## Recursos adicionales
