# Eventos

<!-- TOC depthFrom:4 depthTo:4 -->

- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)
- [EJERCICIO 3](#ejercicio-3)
- [EJERCICIO 4](#ejercicio-4)
- [EJERCICIO 5](#ejercicio-5)
- [EJERCICIO 6](#ejercicio-6)
- [EJERCICIO 7](#ejercicio-7)
- [EJERCICIO 8](#ejercicio-8)

<!-- /TOC -->

## Introducción

Ya hemos aprendido a modificar cosas en nuestra página web mediante JavaScript: cambiar contenidos, estilos, etc. Pero hasta ahora nuestro script (código JavaScript) se ejecutaba al cargar la página. En esta sesión vamos a aprender a hacer nuestra web interactiva, es decir, que haya modificaciones también de contenidos o estilos pero en respuesta a la interacción de la usuaria. La forma de modelar esa interacción de la usuaria en la web es mediante *eventos*. Un evento representa una interacción, que normalmente es de la usuaria, tras la cual podemos realizar una acción. Vamos a ver algunos ejemplos de acciones que implican eventos:
- mostrar una alerta cuando la usuaria hace click en un botón
- cambiar el tamaño de una cabecera fija cuando la usuaria llega a un punto de scroll
- abrir una sección oculta de un formulario cuando hago click sobre un botón
- cerrar una ventana modal cuando termina un temporizador de 15 segundos (aquí no hay acción de la usuaria)
- deshabilitar algunos campos de un formulario, cuando la usuaria selecciona una opción de un select
- enviar una petición al servidor para pedir los datos de los artículos que coinciden con la búsqueda, cuando la usuaria pincha en el botón de buscar en Amazon. Y cuando los datos del servidor llegan al navegador, pintarlos en la página

Es importante entender que nosotros no creamos eventos desde JavaScript sino que un evento se genera pero desde JavaScript podemos saber que ha sucedido. Ejemplos de eventos:
- click en un botón
- scroll en la página
- un cambio el contenido de un input
- expira un temporizador
- llegan los datos del servidor

Lo que podemos hacer desde JavaScript es responder a estos eventos. ¿Cómo? Creando una función que se va a ejecutar cuando el evento sucede. 

Vamos a entender cómo actuamos en JavaScript con los ejemplos anteriores:
- cuando la usuaria hace click en el botón *más info*, ejecutamos una función que muestra un información que estaba escondida
- cuando el usuario hace scroll en la página, ejecutamos una función que comprueba si la posición de la pantalla es mayor que x píxeles y en caso afirmativo aplica una clase CSS a la cabecera

## Escuchando eventos desde JavaScript

Vamos a ver cómo traducimos lo anterior a JavaScript. Escuchar un evento es decirle al navegador: vigila un determinado elemento de HTML, y cuando alguien haga `click` sobre él, ejecuta esta función que he preparado. 
Técnicamente, registramos en el navegador una `función escuchadora` o `listener` sobre un elemento para que ejecute una `función manejadora de eventos` o `handler` cuando el evento suceda. 

Vamos a ver el ejemplo de mostrar una alerta pulsando un botón.

Dado este HTML:

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="utf-8">
    <title>Ejemplo de alerta</title>
  </head>
  <body>
    <button type="button" name="button" class="alert">Alerta</button>
    <script type="text/javascript" src="js/index.js"></script>
  </body>
</html>
```
Para empezar, tendremos recoger de HTML el elemento sobre el que queremos escuchar eventos. Para ello, usaremos nuestro ya habitual `querySelector`.

```js
const button = document.querySelector('.alert');
```

A continuación, vamos a usar el método `addEventListener` de los elementos de HTML para escuchar eventos. Le pasaremos 2 parámetros: el tipo de evento a escuchar y la función que tiene que ejecutar cuando suceda el evento. Primero vamos a definir la función manejadora (`handler`), y luego registramos la función escuchadora (`listener`).

```js
// elemento de HTML
const button = document.querySelector('.alert');

// handler
const showAlert = () => console.log('Alerta');

// listener sobre el elemento, con tipo de evento y handler
button.addEventListener('click', showAlert);
```
[Aquí podéis jugar con el ejemplo en codepen](https://codepen.io/adalab/pen/RjvLXe?editors=1010).

De esta forma, cuando hagamos click sobre el botón se ejecutará la función `showAlert`. Es importante que os fijéis en algunos detalles importantes:
- la función `addEventListener` la registramos sobre `button` que es un elemento de HTML (en este caso un botón)
- el primer argumento que le pasamos a `addEventListener` es una cadena con el nombre del evento, en este caso `click`
- el segundo argumento que le pasamos a `addEventListener` es una función, es decir, ponemos el nombre de la función pero no la ejecutamos (no ponemos paréntesis al final)

Vamos a detenernos un momento aquí: **el segundo argumento es una función**. Y es que en JavaScript podemos pasar el nombre de una función como argumento de otra. Es esta función que recibe el argumento la que se encarga de ejecutarla. Podéis ver un ejemplo en este [pen](https://codepen.io/adalab/pen/xyZexZ?editors=1011).

Observa la diferencia entre la ejecución de una función
 - `logError()`

y el nombre de una función

 - `logError`

Esto os puede parecer un poco raro y complejo al principio, pero iremos descubriendo en el curso que es muy útil. A este tipo de funciones que se pasan como argumentos a otras, se les llama **callbacks**

Por lo tanto la función que le pasamos a `addEventListener` como segundo argumento es un `callback`, no la ejecutamos nosotras, es ejecutada por `addEventListener` cuando sucede el evento.

Para pasar un *callback* como argumento, podemos utilizar el nombre de una función ya declarada (como vimos en el ejemplo anterior), o podemos declararla directamente cuando la pasemos como argumento. Son dos maneras diferentes de hacer lo mismo. Vamos a ver el ejemplo anterior, pero declarando la función cuando la pasamos como argumento.

```js
const button = document.querySelector('.alert');
button.addEventListener('click', function showAlert() {
   console.log('alerta');
});
```
Esta versión tiene sólo 2 líneas y es un poco más enrevesada, pero funciona igual que la anterior. Vamos a verla con una arrow function:

```js
const button = document.querySelector('.alert');
button.addEventListener('click', () => console.log('alerta'));
```

> NOTA:
> Es muy importante entender que la función sólo se ejecutará cuando suceda el evento. Si el evento nunca sucede, la función nunca se ejecutará. Nosotros nunca ejecutamos la función: es el navegador quien la ejecuta cuando sucede el evento.

Existen otras formas de escuchar eventos que veréis por Internet, y que aunque siguen funcionando **no recomendamos** usar. La principal razón es porque queremos separar contenido (HTML), diseño (CSS) y funcionalidad (JavaScript), y al ser funcionalidad debería hacerse desde JS. Estas otras formas de escuchar eventos se basan es el uso del atributo `onclick` (en realidad, on + evento), que pueden usarse desde HTML:

```html
<button type="button" name="button" class="alert" onclick="showAlert()">Alerta</button>
```
O desde JavaScript:

```javascript
const button = document.querySelector('.alert');
button.onclick = function(){
  alert('Alerta');
}
```
A partir de ahora usaremos **siempre, siempre, siempre** la forma correcta, es decir, `addEventListener`.

* * *

#### EJERCICIO 1

**Hola click**

Crear una página HTML con un párrafo en el que ponga Hola y un botón. Usando JavaScript, cambiar ese texto por "Mi primer click, ¡ole yo y la mujer que me parió!" cuando se pulse el botón.

* * *

#### EJERCICIO 2

**¿Cómo te llamas?**

Crear una página HTML con un input de tipo texto para introducir tu nombre y un botón. Al pinchar sobre el botón, imprimir en la consola el mensaje 'Hola <nombre>', con el nombre que aparece en el input de texto.

> **Nota**: La etiqueta `input` no tiene apertura y cierre, por lo tanto técnicamente no tiene contenido. Si para recoger el contenido de una etiqueta con apertura y cierre utilizábamos `innerHTML`, para recoger el valor de un input utilizaremos `value`.

* * *

Aparte del evento click, podéis ver [el listado completo de eventos que podemos escuchar en MDN](https://mdn.mozilla.org/en-US/docs/Web/Events). Aquí vamos a listar algunos de los más usados:
- Eventos de ratón
  - `click`: botón izquierdo del ratón
  - `mouseover`: pasar el ratón sobre un elemento
  - `mouseout`: sacar el ratón de un elemento
- Eventos de teclado
  - `keypress`: pulsar una tecla
- Sobre elementos
  - `focus`: poner el foco (seleccionar) sobre un elemento, por ejemplo un input
  - `blur`: quitar el foco de un elemento
  - `change`: al cambiar el contenido de un input (hay que quitar el foco para que se considere un cambio) o de un select
- Formularios
  - `submit`: pulsar el botón submit del formulario
  - `reset`: pulsar el botón reset del formulario
- De la ventana
  - `resize`: se ha cambiado el tamaño de la ventana
  - `scroll`: se ha hecho scroll en la ventana o un elemento

* * *

#### EJERCICIO 3

**Dame ipsum**

Crear una página HTML con un párrafo con `lorem ipsum`. Al poner el ratón sobre el párrafo, vamos a añadir un nuevo párrafo a la página con `lorem ipsum`.

* * *

## Información sobre el evento

Como hemos visto, cuando registramos un listener para escuchar un evento, es el navegador quien ejecuta la función `handler`. 

Al ejecutarla, le pasa unos argumentos que podremos recoger si definimos parámetros en nuestra función `handler`. El primero de ellos es un objeto que se suele denominar y que contiene información acerca del evento. 
Aun no hemos visto los objetos, pero ahora mismo basta decir que son como una variable con muchas variables dentro.

```js
const buttonElement = document.querySelector('.button');

function handleButtonClick(event) {
  console.log(event);
}

buttonElement.addEventListener('click', handleButtonClick);

```
Vamos a ver alguna de la información útil que contiene:

### event.currentTarget

En **`event.currentTarget`** encontraremos el **elemento sobre el que pusimos el listener**.

```html
<button class="button__add-one">
0
</button>
```

```js

const plusOneButtonElement = document.querySelector('.button__add-one');

function handlePlusOneButton(event) {
  // Recogemos el elemento sobre el que pusimos el listener
  // y lo asignamos a una constante
  const buttonElement = event.currentTarget;
  buttonElement.innerHTML = parseInt(buttonElement.innerHTML) + 1;
}

plusOneButtonElement.addEventListener('click', handlePlusOneButton);

```
Como ya habrás notado en el ejemplo anterior las constantes `plusOneButtonElement` y `buttonElement` tienen asignado el mismo elemento de HTML. 
Entonces ¿para qué queremos `currentTarget`, si nosotras hemos puesto el listener y por lo tanto ya sabemos cual es elemento botón?
Para poder diferenciar entre dos elementos que tienen un listener con el mismo `handler`. Así podemos tener una sola `función manejadora` para dominarlos a todos :)

Un caso muy claro sería un listado de elementos en el que queremos que, al pinchar sobre un elemento, este y solo este cambie de estilo. 

[Ejemplo](https://codepen.io/adalab/pen/XxdPWL) de una lista que permite marcar como añadida una fruta en un carro de la compra de una frutería.

* * *

#### EJERCICIO 4

**¿Qué vemos esta noche?**

Vamos a partir de un HTML con un botón 'Empezar'. Al hacer click, vamos a pintar en el HTML un listado de películas que tenemos en JavaScript:
```js
const inception = 'Inception';
const theButterFlyEffect = 'The butterfly effect';
const eternalSunshineOfTheSM = 'Eternal sunshine of the spotless mind';
const blueVelvet = 'Blue velvet';
const split = 'Split';
```
Después vamos a escuchar eventos sobre cada elemento de la lista, de forma que al hacer click sobre el nombre de una película aparezca en la consola el nombre de esa película.

* * *

#### EJERCICIO 5

**Favoritos**

Hemos preparado un [HTML](https://codepen.io/adalab/pen/xyEwVj) con tres tarjetas. 
Al pinchar en un elemento del listado tenemos que:

- En el `li` añadir la clase `.teacher--selected` si no la tiene, o quitarla si la tiene.
- Modificar el texto del span `.favorite` sustituyéndolo por 'Quitar' si en ese momento contiene 'Añadir', o por 'Añadir' si contiene 'Quitar'.

> **Nota 1**: con `querySelector` buscamos un elemento dentro de otro. Hasta ahora lo habíamos usado para buscar dentro de `document` (todo nuestro documento HTML), con `document.querySelector()`. 

> Si tuviéramos una constante llamada, por ejemplo, `sectionAboutElement` en la que hemos guardado un elemento de HTML, podríamos buscar dentro de este otro elemento, tal que así `sectionAboutElement.querySelector()`

> **Nota 2**: para facilitar añadir y quitar clases de CSS, os recomendamos usar `classList.toggle`

* * *

#### EJERCICIO 6

**Jugando con el teclado**

Tenemos que crear una página vacía. Al pulsar la tecla 'r' su color de fondo cambia a rojo y al pulsar la 'm' a morado. Vamos a escuchar un evento de teclado (directamente sobre el elemento `document`). En el evento podemos [consultar la propiedad `key`](https://keycode.info/) para saber qué tecla se ha pulsado.

* * *

### event.target

En **`event.target`** encontraremos el **elemento sobre el que ha sucedido el evento**. Este elemento no tiene por que ser el mismo sobre el que pusimos el listener. 

Recordemos que en HTML se anidan las etiquetas, de manera que si ponemos un listener de `click` sobre un `div padre` que contenga varios `spans hijos`, al hacer click sobre cualquiera de los hijos, **en target estará el span hijo sobre el que se ha hecho click** y **en currentTarget el div padre sobre el que pusimos el listener**.

* * *

#### EJERCICIO 7

**Delegando eventos**

Vamos a `refactorizar` el [EJERCICIO 4](#ejercicio-4) para mejorarlo utilizando la técnica `event delegation`. Tenemos que quitar ese mogollón de listeners en los `li`s y reemplazarlos por uno solo en la etiqueta madre (`ul`).
¡A por ello!

* * *


### event.preventDefault()
Algunos elementos de HTML tienen comportamientos por defecto ante eventos, por ejemplo:

- al hacer click en un input de tipo checkbox este se marca/desmarca
- al hacer click en un botón o un input de tipo submit que se encuentra en un formulario el navegador intenta enviar los datos al servidor
- al hacer click en un enlace navegamos al mismo

El método **`event.preventDefault()` nos permite prevenir** estos **comportamientos por defecto** desde JavaScript.

Uno de los casos más comunes es prevenir el envío de un formulario.

Aunque aún no hemos visto como enviar un formulario desde JavaScript, prevenir que lo envíe el navegador sería el primer paso para poder controlarlo, validando sus datos, enviándolos al servidor desde JavaScript y mostrando _feedback_ a la usuaria sobre el proceso.

- [Ejemplo de botón submit en un formulario](https://codepen.io/adalab/pen/bjwJGv)

* * *

#### EJERCICIO 8

**Para ese link**

¿Recuerdas el proyecto del sprint uno? Los enlaces de la cabecera de nuestra página tenían un problema, como nuestra cabecera era flotante, al navegar a una sección parte del contenido de quedaba oculto tras la cabecera. 

Vamos a animarnos y a preparar un HTML muy sencillo con:
- una cabecera flotante que contenga un menu con tres enlaces 
- tres secciones con bastante 'loreipsum' para que haya un scroll generoso

El primer paso para arreglar este comportamiento es escuchar el click en los enlaces y prevenir el comportamiento por defecto.

Hhhmm, pero entonces no pasa nada al hacer click... Correcto, ¡ejercicio terminado!

> **Nota**: no te preocupes, veremos cómo hacer que esos enlaces acaben de funcionar en futuras lecciones.

* * *

## Dejando de escuchar eventos

Puede llegar un punto en que queramos dejar de escuchar eventos sobre un elemento. Para eso usaremos la función `removeEventListener` pasándole los mismo parámetros que al registrarlo.

```js
const buttonElement = document.querySelector('.alert');
buttonElement.removeEventListener('click', showAlert);
```

## BONUS

## Burbujeo de eventos o `event bubbling`

Cada vez que sucede un evento sobre un elemento de HTML, este 'burbujea' hacia arriba. Esto quiere decir que el evento sucede en ese elemento, y después en el elemento padre, y después en el abuelo, y así hasta llegar al último ancestro, `html`.

Aunque no lo vemos, esto está sucediendo continuamente en el navegador, por ejemplo cada vez que movemos el ratón, o hacemos click en cualquier sitio. este comportamiento hace que:
 - podamos 'escuchar' un evento en un elemento, sin que esto implique que se haya iniciado en él
 - podamos poner `listeners` con `handlers` en varios padres y que todos se ejecuten si sucede un evento en un hijo común

Pincha en los `divs` de este [codepen](https://codepen.io/adalab/pen/MPjyyW?editors=1010) y observa como se comportan.

Esto nos permite técnicas tan interesantes como `event delegation` que practicamos en el [EJERCICIO 7](#ejercicio-7), con la cual podemos poner un listener en un `ul` y así manejar los eventos sobre sus hijos `li`s.

En este [pen](https://codepen.io/adalab/pen/zLKwwP) puedes ver como manejar eventos anidados sin que entren en conflicto.

## Resumen

En esta sesión hemos visto: como hacer nuestras webs interactivas de verdad, escuchando eventos y reaccionando a ellos gracias a `addEventListener(type, handler)`. Como utilizar información que nos devuelve el navegador sobre los eventos:

- `event.currentTarget`: elemento con el listener
- `event.target`: elemento sobre el que sucede el evento
- `event.preventDefault()`: método para prevenir el comportamiento por defecto de un evento sobre un elemento

También, nos hemos acercado a los conceptos: 

- `event bubbling`: los eventos pasan de unos elementos a otros de manera ascendente
- `event delegation`: gracias al burbujeo de los eventos podemos poner `listeners` a elementos padres para controlar eventos en hijos

Y hemos visto nueva información que no es exclusiva de los eventos como:

- `classList.toggle`: quita o añade una clase de CSS
- `inputNameElement.value`: nos devuelve el valor de un input
- `callback`: una función ejecutada por otra función

## Recursos externos

- [key codes info](https://keycode.info/)
- [Introduction to event listeners](https://www.youtube.com/watch?v=EaRrmOtPYTM&list=PLyuRouwmQCjnEupVi5lpP6VrLg-eO-Zcp&index=1)
- [classList.toggle](https://alligator.io/js/classlist/#toggle)
