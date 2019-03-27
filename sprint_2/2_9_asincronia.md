# Métodos de array y temporizadores

<!-- TOC depthFrom:4 depthTo:4 -->

- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)
- [EJERCICIO 3](#ejercicio-3)
- [EJERCICIO 4](#ejercicio-4)
- [EJERCICIO 5](#ejercicio-5)
- [EJERCICIO 6](#ejercicio-6)
- [EJERCICIO 7](#ejercicio-7)
- [EJERCICIO 8](#ejercicio-8)
- [EJERCICIO 9](#ejercicio-9)
- [EJERCICIO 10](#ejercicio-10)
- [EJERCICIO 10](#ejercicio-10)
- [EJERCICIO 11](#ejercicio-11)
- [EJERCICIO 12](#ejercicio-12)
- [EJERCICIO 13](#ejercicio-13)
- [EJERCICIO 14 BONUS](#ejercicio-14-bonus)
- [EJERCICIO 15 BONUS](#ejercicio-15-bonus)
- [EJERCICIO 16 BONUS](#ejercicio-16-bonus)
  <!-- /TOC -->

## Introducción

En esta sesión vamos a seguir profundizando en el uso de arrays para manejar listados de datos. Aprenderemos métodos de array muy útiles que nos proporciona el lenguaje Javacript para poder almacenar nueva información en un array y procesar los datos que contiene.

Durante esta sesión vamos a ver cómo se ejecutan las órdenes en JavaScript para entender mejor cómo funciona el lenguaje, para ello veremos qué es eso de la asincronía y por qué es una de las características más importantes de JavaScript.

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

## ¿Qué es la asincronía?

Imaginemos que tenemos un conjunto de tareas a realizar. En los lenguajes tradicionales, ese conjunto de instrucciones se realizaba una tras otra, es decir, imaginemos que tenemos los siguientes pasos:

1. Mostrar un mensaje en la pantalla
2. Realizar una petición al servidor
3. Mostrar otro mensaje
4. Con la respuesta del servidor, mostrar "Respuesta: ..."

En un lenguaje tradicional, se ejecutarán de forma secuencial, es decir, una tarea tras otra. Primero el paso 1, cuando termine, el paso 2 y así sucesivamente. De esta forma si realizamos una petición en el paso 2, hasta que no se reciba la información (que podría tardar varios segundos), no podríamos mostrar el mensaje del paso 3.

Pensemos por un momento en qué supone que cada paso se ejecute uno detrás de otro en la web. En primer lugar, si solicitamos una información a un servidor, durante el tiempo entre que se pide esa información y la respuesta no se podrá ejecutar nada de JavaScript, porque estará parado el resto del código hasta el momento de recibir la información del servidor. Cuando decimos nada de JavaScript, esto también implica que si tenemos algo de código que se va a ejecutar al pulsar un botón este tampoco funcionará y eso se traduce en que no se podrá interactuar con la web.

Pensad en Google Maps o Google e imaginaos lo que supondría que cada petición que hace al servidor (cargar una parte del mapa o recargar un nuevo resultado) hiciese que la página se congelase. Sería algo totalmente contraproducente. De este hecho nació la necesidad de hacer algo que no parase nuestro código cuando se realiza la petición a un servidor, nació la asincronía.

JavaScript permite realizar tareas de forma asíncrona y concurrente, esto quiere decir que pueden realizarse tareas que no vayan en cadena y ejecutarse ambas a la vez y trabajar de forma independiente.

Si mantenemos el caso anterior, en el caso de JavaScript se hará lo siguiente. Se ejecutará el paso 1 para mostrar un mensaje en la pantalla, se realizará luego el paso 2, que hará una petición al servidor y aquí es donde recae la diferencia. Como hemos dicho antes, en JavaScript no puede quedarse una orden esperando hasta que se ejecute la actual cuando se trata de tareas de larga duración. Para resolver esto, el navegador delega algunas tareas en otros procesos y mientras continúa con las siguientes. Así que se ejecutarán el resto de tareas hasta que llegue la petición del servidor, cuando se ejecutará el código con el resultado.

### ¿Por qué es importante entender la asincronía?

Entender la asincronía en JavaScript será fundamental para saber en qué orden se ejecutará nuestro código y por tanto, poder lidiar con él mejor sin que tengamos problemas de que algún paso no se ejecute cuando lo necesitamos.

Además, la mayoría de las formas de hacer nuestra web interactiva (eventos) dependen de esa asincronía por lo que supone un conocimiento muy importante si queremos hacer que nuestra web sea interactiva y funcione correctamente.

### Ejecutar código pasado un cierto intervalo de tiempo

En esta sección vamos a ver cómo podemos ejecutar en JavaScript pasados determinados milisegundos. Esto nos será muy útil para realizar webs como Kahoot, en la que tenemos un máximo de tiempo y cada x segundos el contador de tiempo disminuye.

Otros ejemplos de uso podrían ser cerrar la sesión de una web transcurridos X segundos, por ejemplo. Cualquier cosa que dependa del tiempo en una página probablemente se ejecute con el código que vamos a ver a continuación.

### setInterval

En JavaScript podemos crear código para que se ejecute cada determinado tiempo, para ello utilizamos `setInterval()`.

Esta función recibe 2 parámetros:

- la función a ejecutar cada cierto tiempo (sin paréntesis como hacíamos en addEventListener, ya que no la ejecutamos nosotras)
- el tiempo en milisegundos

Vamos a ver un ejemplo: un contador que se incrementa cada segundo y se muestra en pantalla.

```html
<p class="time">0</p>
```

En el HTML tenemos un párrafo con la clase `time`.

```javascript
let counter = 0;

const incrementAndShowCounter = () => {
  counter++;
  const time = document.querySelector('.time');
  time.innerHTML = counter;
};

setInterval(incrementAndShowCounter, 1000);
```

En JavaScript definimos una variable global que será nuestro contador. También una función que incrementa el contador y lo muestra en el HTML, que será la que ejecutemos cada cierto tiempo. Finalmente ejecutamos la llamada a `setInterval` pasando como primer parámetro la función y luego 1000 para indicar que se ejecute cada segundo.

> NOTA: En el ejemplo anterior pasamos a `setInterval` la función `incrementAndShowCounter` como argumento, sin ejecutarla. A estas funciones en JavaScript se les suele llamar _callbacks_.

Podéis [jugar con el código de este ejemplo en Codepen](https://codepen.io/adalab/pen/POLdmN?editors=1010#0).

Para obtener más información acerca de `setInterval`, consultaremos la [documentación de setInterval en MDN](https://developer.mozilla.org/es/docs/Web/API/WindowTimers/setInterval).

---

#### EJERCICIO 5

Partiendo del ejemplo anterior, vamos a realizar un temporizador que empiece en 0 y cada 2 segundos se incremente.

---

#### EJERCICIO 6

Todos sabemos lo que pasó en Canal Sur hace unos años, en mitad de las campanadas pusieron anuncios y aguaron la noche a millones de personas. Para estar preparados, vamos a crear un contador de uvas. Este contador empezará en 0 y cada segundo incrementará en 1, así hasta 12, en ese momento terminará la cuenta y se dejará de contar más.

La cuenta se mostrará en la pantalla con números y si lo deseas puedes añadir una imagen de una uva cada vez que pase un segundo.

> PISTA: la función se puede seguir ejecutando con setInterval pero para que se pare en 12 basta con dejar de pintar en el HTML en el momento adecuado.

---

#### EJERCICIO 7

Vamos a realizar el típico mensaje que aparece en un blog con la información de hace cuanto se escribió un post. Por ejemplo, con el texto: "escrito hace 30 segundos". Al principio escribiremos en pantalla "escrito hace 1 segundo" e iremos aumentando el número de segundos. Cuando lleve más de 59 segundos queremos que ponga "escrito hace 1 min".

---

### setTimeout

El método `setTimeout()` es muy similar a `setInterval()` pero a diferencia de este solo ejecuta una vez la función que le pasemos. Sirve entonces para retrasar determinados milisegundos una operación.

Por ejemplo, vamos a crear un texto de aviso de que algo se ha guardado correctamente. Este mensaje se borrará pasados 6 segundos.

```html
<p class="msg">Se ha guardado correctamente</p>
```

En HTML sólo tenemos un párrafo con el mensaje de confirmación y la clase `msg`.

```javascript
const removeMsg = () => {
  const msg = document.querySelector('.msg');
  msg.innerHTML = '';
};

setTimeout(removeMsg, 6000);
```

En JavaScript definimos la función que elimina el mensaje de la pantalla. Luego llamamos a `setTimeout` para que ejecute esa función pasados 6 segundos.

Podéis [jugar con este ejemplo el Codepen](https://codepen.io/adalab/pen/EbMeOM).

Para obtener más información acerca de `setTimeout()`, consultaremos la documentación de MDN:

- [Documentación de setTimeout en MDN](https://developer.mozilla.org/es/docs/Web/API/WindowTimers/setTimeout)

---

#### EJERCICIO 8

Con JavaScript, crear un código para mostrar una ventana en nuestro navegador una vez transcurridos 15 segundos que ponga "su sesión ha expirado" (creada usando HTML y CSS).

---

### Cancelar eventos de setInterval y setTimeout

En algunas ocasiones querremos dejar de realizar una tarea que hemos configurado con `setInterval` para que se realice cada determinado tiempo o cancelar una tarea programada con `setTimeout`. Para ello utilizaremos los métodos `clearTimeout` y `clearInterval`.

Vamos a partir del ejemplo anterior del contador que se actualizaba cada segundo. Queremos que a los 10 segundos se pare, eliminando la ejecución de la función con setInterval.

```javascript
let counter = 0;
let temp;

const incrementAndShowCounter = () => {
  counter++;
  const time = document.querySelector('.time');
  time.innerHTML = counter;
  if (counter === 10) {
    clearInterval(temp);
  }
};

temp = setInterval(incrementAndShowCounter, 1000);
```

Hemos hecho sólo un par de cambios en JavaScript. En primer lugar hemos guardado el identificador del temporizador en una variable `temp` para que luego sea accesible desde la función. El segundo cambio es que ahora en la función hacemos una comprobación y si el contador llega a 10 ejecutamos el `clearInterval` y la función deja de ejecutarse cada segundo.

Podéis [jugar con este ejemplo el Codepen](https://codepen.io/adalab/pen/ooVPOg).

Para obtener más información:

- [clearInterval](https://www.w3schools.com/jsref/met_win_clearinterval.asp)
- [clearTimeout](https://www.w3schools.com/jsref/met_win_cleartimeout.asp)

---

#### EJERCICIO 9

Vamos a modificar nuestra solución del ejercicio 6 para que, en lugar de seguir ejecutando la función indefinidamente, detengamos su ejecución con `clearInterval`.

---

#### EJERCICIO 10

Crear un cronómetro que vaya aumentando en segundos y cuando se pulse el botón de parar deje de aumentar. Cuando pulsemos el de continuar, vuelva a empezar de nuevo.

---

#### EJERCICIO 11

Crear una página con un botón que transcurridos 10 segundos te pregunte: "¿te has dormido?". Si pulsas en el botón la cuenta volverá a cero y otra vez, si transcurren 10 segundos sin pulsar volverá a preguntar de nuevo "¿te has dormido?"

---

#### EJERCICIO 12

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

En los videos que enlazamos a continuación, se explica de forma más detallada qué es la asincronía y cómo funciona ésta en JavaScript.

- [Asincronía en JavaScript - Parte 1 - Sincronía y Concurrencia](https://www.youtube.com/watch?v=PndHsDpEfhU)
- [Asincronía en JavaScript - Parte 2 - Event loop](https://www.youtube.com/watch?v=rgmej4Jx4WM)

---

#### EJERCICIO 13

Usando la herramienta [loupe](http://latentflip.com/loupe/?code=!!!PGJ1dHRvbj5DbGljayBtZSE8L2J1dHRvbj4%3D) que se utiliza en el video (ver el vídeo), realizar en JavaScript las siguientes tareas para ver en qué orden se reproducen:

TAREAS A

1. Crear una función `funA` que contenga un `console.log('hola')`
2. Crear otra función `funB` que ejecute `funA`
3. Ejecutar la función `funB`

TAREAS B

1. En un if comprobar si "Hello" y "hello" son iguales
2. Si lo son, ejecutar un `console.log` que diga "lo son"
3. Si no lo son, ejecutar un `console.log` que diga "no lo son"

TAREAS C

1. Crear una función `pulsado()` que guarde en una variable el texto "pulsado" y luego muestre esa variable con un `console.log`
2. Crear un botón que llame a la función anterior. Podemos editar el HTML en el panel inferior izquierdo. Usaremos una sintaxis propia del programa en lugar de `addEventListener`:
   `$.on("button", "click", pulsado);`

3. Añadir un `console.log` al final que muestre el texto "empezamos"

¿Sabrías explicar por qué se ejecutan en ese orden? En caso de no ser así consulta y debate con el resto de tus compañeras.

---

## BONUS

#### EJERCICIO 14 BONUS

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

#### EJERCICIO 15 BONUS

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

#### EJERCICIO 16 BONUS

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

- [Javascript Asíncrono: La guía definitiva](https://lemoncode.net/lemoncode-blog/2018/1/29/javascript-asincrono)
