# Peticiones al servidor 2

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
- [EJERCICIO 10 BONUS](#ejercicio-10-bonus)

<!-- /TOC -->

## Introducción

En esta sesión vamos a tratar varios temas diferentes: 1) las APIs, concepto que ya conocemos, pero vamos a entender un poco mejor cómo funcionan; 2) el localStorage, un sistema de almacenamiento de datos en el navegador y 3) el linter, una herramienta que nos ayuda a mejorar nuestro código JavaScript.

*API* viene de *Application Programming Interface*, es decir, es una interfaz que está pensada para ser accedida desde una aplicación de código. Dicho de otra forma, el servidor define una forma de pedirle datos, pensada para que sea una aplicación (un programa) quien los pida y él sepa enviárselos. Hay otras interfaces, como una página web, que están pensadas para ser usadas por personas. Pero las APIs están pensadas para ser usadas desde la programación, en nuestro caso desde nuestro programa JavaScript. Durante esta sesión vamos a ver varios ejemplos de APIs.

Un *linter* es una herramienta que nos sirve para prevenir errores y nos ayuda a mantener un estilo homogéneo en nuestro código. Veremos cómo usar un linter para JavaScript llamado *ESLint* y cómo integrar los mensajes que nos manda en nuestro editor de código, en este caso Code.

## ¿Para qué sirve lo que vamos a ver en esta sesión?

Entender mejor el concepto de API y ver ejemplos nos ayudarán a entender mejor cómo trabajar con ellas. Además, entenderemos mejor cómo están construidas y cómo se espera que las usemos gracias a conocer mejor el protocolo HTTP que es el usado en Internet.

Usar un linter en nuestro proyecto nos sirve para que mientras desarrollamos un código JavaScript mantengamos una coherencia de estilos con el resto del equipo. También nos sirve para poder detectar errores típicos al escribir código, por ejemplo, si tengo variables no usadas o estoy usando variables antes de declararlas.


## ¿En qué casos se utiliza?

Las APIs van a estar presentes en prácticamente cualquier desarrollo web que hagamos porque, al final de todo, es casi seguro que tengamos que enviar y recibir datos de un servidor. Si se ha diseñado bien, en la interfaz de comunicación de ambos (frontend y backend) debería haber un API.

Utilizaremos un linter en un entorno de trabajo donde una o varias personas estamos trabajando sobre una base de código y/o queramos mantener unas reglas de estilo concretas (cuando trabajamos en solitario sigue teniendo sentido usarlo). Por ejemplo, qué indentación de código usar o el uso de los punto y coma.


## El mundo de las APIs

Como ya hemos dicho, las APIs son la forma en que desde un programa (en nuestro caso un código JavaScript en el frontend) podemos acceder a datos en un servidor web, que están en un backend (un servidor, es decir, un ordenador conectado a Internet). En el backend normalmente tendremos un programa ejecutándose, que podría estar escrito en distintos lenguajes de programación (PHP, python, ruby, Node...), y que tiene acceso a una base de datos (una base de datos es un tipo especial de programa que sirve para almacenar datos y poder consultarlos). Pero a nosotros nos da igual el lenguaje de programación en que esté escrito el backend, lo que nos importa es que **podemos interactuar con él a través de una URL**.

Como vimos en la sesión anterior, haciendo una petición con `fetch` a una URL del servidor conseguíamos obtener datos, desde fotos de perros hasta los repos de una organización en GitHub. Por tanto el servidor de una aplicación web (página web que maneja datos dinámicos) tiene establecida una API, es decir, un conjunto de URLs especiales con las que podemos interactuar desde nuestro programa para consultar y almacenar datos. Estas URLs no están escogidas al azar sino que siguen una serie de convenciones a la hora de crearse. La convención más usada para la creación de APIs se llama REST (*REpresentational State Transfer*) por eso muchas veces oiremos hablar de **APIs REST**. La convención que define REST está basada en HTTP, el protocolo de comunicación entre los ordenadores de la web (la World Wide Web - WWW). Estos dos acrónimos seguro que nos suenan mucho porque los escribimos millones de veces al escribir un URL en nuestro navegador web.

### Un poquito de HTTP

Las máquinas que están conectadas a Internet para entenderse entre ellas utilizan un protocolo, es decir, una forma estándar de enviarse información para poder entenderse. HTTP viene de *Hyper Text Transfer Protocol*, en español protocolo para transferencia de hiper-texto, es decir, para que las máquinas intercambien información entre ellas más allá del simple texto (texto, imágenes, videos, etc).

La forma de funcionar de HTTP es mediante **petición y respuesta**. Un ordenador hace una petición (el que llamamos cliente, en nuestro caso desde navegador) y otro ordenador (el que llamamos servidor) recibe esa petición, la procesa (hace cosas) y envía de vuelta una respuesta.

La **petición**, como hemos visto en los ejemplos de la sesión anterior, siempre lleva asociada una URL que indica dónde está el servidor y el tipo de datos que le pedimos. Por ejemplo la URL `https://api.rand.fun/text/password?length=20` de una petición a RandAPI nos muestra que
- el servidor del API está en `https://api.rand.fun/` (se le llama normalmente *URL base*)
- el servicio (tipo de datos que pedimos) al que accedemos es `text/password` y, en este caso, nos da una cadena aleatoria como contraseña
- los parámetros `?length=20` (también llamado *querystring*) indican que la longitud de la cadena que pedimos es 20

La petición HTTP también tiene asociada un *método* que indica la *intención* con la que hacemos la petición. Los métodos (o verbos) más usados son *GET* y *POST*. *GET* lo usamos para decir al servidor que esa petición es para consultar datos que él ya tiene, como por ejemplo las fotos de perros. *POST* lo usamos para enviar nosotros datos al servidor. Si recordáis estos mismo métodos los podíamos definir para el método de envío de un formulario HTML que sirve para enviar datos al servidor. Existen otros métodos HTTP, por ejemplo, *PUT* y *PATCH* sirven para actualizar datos ya existentes en el servidor, y *DELETE* sirve para borrar datos.

 El método HTTP junto a la URL es lo que define la acción que queremos realizar en el servidor según la convención de REST. Aquí vemos algunos ejemplos de un API para manejar información de usuarios:
- petición `GET` a la URL `/users`: el servidor devuelve un listado (array) de usuarios
- petición `GET` a la URL `/users/1`: el servidor devuelve un la información del usuario cuyo id es 1
- petición `POST` a la URL `/users` con los datos de un usuario: el servidor crea un usuario nuevo

Otra característica habitual de un API REST es que cuando accedo a un listado de cosas, si hay muchas, no me devuelva todas en la misma petición sino que me devuelve solo las primeras. A esto se le llama *paginación* y al hacer la petición recibiré solo *la primera página* de resultados, por ejemplo 10. Y tendré que añadir un parámetro a la *querystring* para recuperar el resto de páginas, por ejemplo, `?page=2`.

* * *
#### EJERCICIO 1

Vamos a explorar [un API abierto de información sobre el mundo Star Wars](https://swapi.co/). En esta página tenemos la documentación completa del API y un formulario que nos permite hacer peticiones a la URL que indiquemos. Identifica la siguiente información sobre SWAPI:
- la URL base del API
- si necesita autenticación
- método HTTP que deben usar las peticiones a este API
- URL para acceder a la info del personaje "Luke Skywalker"
- URL para acceder a la info de la película "A New Hope"
- a qué otros recursos puedo acceder desde el API además de personajes y pelis
- URL para acceder al listado de personajes, ¿está paginada?
- cómo puedo buscar personajes mediante la URL
- cómo puedo hacer que el JSON de una petición se me devuelva traducido a Wookiee

* * *

#### EJERCICIO 2

Ahora que conocemos mejor el API de Star Wars vamos a hacer una sencilla web usándolo. En la web aparece una caja de texto donde escribimos el nombre de un personaje (o parte del nombre) y un botón, al hacer click, nuestra web muestra debajo un listado con los personajes que coinciden con la búsqueda indicando su nombre y género.

* * *

Seguimos aprendiendo un poco de HTTP. Para poder hacer una petición compleja con `fetch` tenemos que pasar un segundo parámetro para establecer opciones, donde podemos indicar
- *el método*, por ejemplo, `method: 'POST'` (por defecto es *GET*)
- *datos a enviar*, que son los datos que enviamos al servidor, por ejemplo, `body: '{adalaber: 1}'`
- *cabeceras HTTP*, que son *metadatos* (datos sobre los datos a enviar), como por ejemplo el tipo de los datos que enviamos que puede ser en JSON o en texto plano

Puedes leer más detalles en [el tutorial de uso de `fetch` en MDN](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch).

**¡Vamos a parar un momento!** ¿Entonces me estás diciendo que muchas aplicaciones web, como Twitter o GMail, tienen un API al que yo puedo acceder desde mi programa en JavaScript? ¿Y que a través de un API yo puedo no solo consultar datos sino también enviarlos? ¿Qué me impide entonces enviar un tweet en Twitter como si fuera Pedro Sánchez?

Pues porque las APIs normalmente requieren de una *autenticación*, es decir, que tengas que identificarte de alguna forma desde tu programa para que tus peticiones funcionen. Por ejemplo, en el API de GitHub que ya hemos usado podemos consultar datos sobre los repositorios públicos de Adalab. Pero no podemos, por ejemplo, crear un repositorio nuevo porque necesitamos ser miembro de la organización para poder hacerlo. En este curso por simplicidad vamos a trabajar con APIs abiertas, es decir, que no requieren autenticación y normalmente nos van a servir solo para consultar datos pero no para modificarlos.

* * *

La **respuesta** HTTP que viene del servidor tiene más información además de los datos que le hemos pedido. Uno de ellos es el código del estado de la respuesta, en inglés *HTTP status code*. Existe un estándar definido para saber qué indica este código, y los principales son:
- 200: las respuestas con código 2xx (doscientos y lo que sea) indican que la petición ha ido bien (OK)
- 400: las respuestas con código 4xx (cuatrocientos y pico) indican que ha sucedido un error en la petición; por ejemplo, que el usuario no ha enviado todos los datos que el servidor necesita, o que no está autorizado a acceder a a ese servicio
- 500: las respuestas con código 5xx (quinientos y pico) indican que el servidor ha tenido un error (¿os suena la ballena de Twitter? 😜)

Si queréis profundizar en los código de respuesta HTTP, [qué mejor que hacerlo con gatitos](https://http.cat/).

### Herramientas para trabajar con APIs

No todas las APIs tienen una web como la del SWAPI para poder probar las peticiones. Con la herramienta [Postman](https://www.getpostman.com/) podemos hacer eso mismo nosotras: realizar peticiones a un servicio cambiando la URL, el método HTTP, los datos, las cabeceras, etc.

Otra herramienta fundamental son las propias DevTools del navegador en la pestaña *Network*.

![Devtools Network](assets/images/2-10/devtools-network.png)

* * *

#### EJERCICIO 3

En la página de SWAPI o en la que habéis creado en el ejercicio 2 inspecciona las peticiones que has hecho al servidor. Al abrir la pestaña Network aparece vacía así que comienza a hacer peticiones con la pestaña abierta. Con la información que obtienes de esta pestaña averigua:
- dónde está el método de petición
- el código de la respuesta (recuerda que 200 es OK)
- en las cabeceras de la petición busca una llamada `user-agent`, ¿qué puedes decir de su contenido?
- la respuesta del servidor en JSON
- al recargar la página aparecen un montón de peticiones en la pestaña Network, ¿sabrías filtrar solo las que son de AJAX? Pista: antes de `fetch` las peticiones se hacían con el objeto `XMLHttpRequest` (XHR)

* * *

## LocalStorage

Una característica muy interesante a la que podemos acceder con JavaScript es la posibilidad de guardar datos en el propio navegador. Esto se hace mediante el llamado **LocalStorage** o **SessionStorage**. El primero que permite almacenamiento permanente de datos, y el segundo solo para una sesión. Es decir, si cerramos la página se borrarán. En el curso solo vamos a explicar localStorage pero sessionStorage tiene un uso similar.

Hasta ahora, la única fuente de datos que hemos usado es un API en el servidor, pero con localStorage podemos almacenar también datos en local, es decir, en el propio navegador del usuario. De esta forma, vamos a poder guardar algunos datos interesantes solo para este usuario y que mejore su experiencia en nuestra página. Algo habitual es *cachear* datos del servidor, es decir, guardar algunos datos que obtenemos del servidor de forma que la próxima vez que lo necesitemos no tengamos que hacer una petición sino recogerlo directamente del almacenamiento local. Por ejemplo, en mi web de perros tengo un listado de las razas que obtengo del servidor y lo guardo en local porque es algo que nunca va a cambiar. De esta forma, la próxima vez que entre en la página voy a comprobar si tengo guardada información en local y si la hay así me evito una petición al servidor y la página va más rápido.

Usar el localStorage es bastante sencillo: solo necesitamos un nombre (clave) y unos datos (valor).

### localStorage.setItem

Para guardar datos es tan sencillo como usar `setItem` cuyo primer parámetro es el nombre que le ponemos a los datos y luego los datos que queremos guardar, que pueden ser de cualquier tipo primitivo (cadena, número, booleano). Por ejemplo:

```js
localStorage.setItem('name', 'Ana');
```

### localStorage.getItem

Para recuperar los datos es tan sencillo como usar `getItem` y pasar el nombre que le dimos a los datos. Por ejemplo:

```js
const name = localStorage.getItem('name');
console.log(name); //Ana
```

### localStorage.removeItem

Para borrar los datos es tan sencillo como usar `removeItem` y pasar el nombre que le dimos a los datos. Por ejemplo:

```js
localStorage.removeItem('name');
```

Podemos ver los datos guardados usando las devTools en la pestaña "Application":

![DevTools localStorage](assets/images/2-10/devtools-localstorage.png)

### Guardando arrays y objetos

En localStorage solo podemos guardar datos de tipo primitivo (número, cadena, booleano). ¿Qué pasa si queremos guardar un array o un objeto? Pues necesitamos convertirlo a una cadena para poder guardarlo.

Para eso existe una función en JavaScript `JSON.stringify` que convierte un objeto literal o un array en una cadena. Para realizar la acción contraria, es decir, pasar de una cadena que tiene la información de un objeto a un objeto JavaScript usamos `JSON.parse`. Vamos a ver un ejemplo:

```js
const  tasks = [
  {name: 'Recoger setas en el campo', completed: true},
  {name: 'Comprar pilas', completed: true},
  {name: 'Poner una lavadora de blancos', completed: true},
  {name: 'Aprender cómo funcionan los objetos de JavaScript', completed: false}
];

localStorage.setItem('tasks', JSON.stringify(tasks));

const savedTasks = JSON.parse(localStorage.getItem('tasks'));
console.log(savedTasks.length); //4
```

* * *

#### EJERCICIO 4

**Conociendo LS**

Escribir datos en formularios es muy tedioso para los usuarios. ¡Vamos a cachearlos para facilitarles la vida! 

- Prepara un `input` de texto para el nombre y un párrafo vacío
- Cada vez que la usuaria escriba su nombre (`keyUp`) tenemos que pintar el valor en el párrafo y guardarlo en `localStorage`.
- Al recargar la página tenemos que consultar `localStorage` y, si hay algún nombre guardado, rellenar el input y el párrafo.

* * *

#### EJERCICIO 5

**Buenas prácticas trabajando con LS**

Partiendo del ejercicio anterior vamos a visitar la página y borraremos el valor del `localStorage` a través de las DevTools. Con el `localStorage` limpito, recargaremos la página para simular la primera visita de la usuaria, dónde aun no habría información sobre el nombre guardada (`cacheada`). 

Si al realizar esta acción nos encontramos algún error tenemos que apañarlo.

A partir de ahora **recuerda** que siempre que recojas un dato del localStorage, deberías comprobar que existe antes de empezar a trabajar con el, y **realizar una limpieza del localStorage** manual para comprobar que todo funciona como esperas, haya o no datos cacheados.

* * *

#### EJERCICIO 6

**Mi tema preferido**

Vamos a preparar una página sencilla, con un título, un par de párrafos y un selector de tema. Para hacer el selector:

- Añadiremos dos `radio buttons` para poder elegir entre claro y oscuro.
- Prepararemos dos clases de css: una pondrá el fondo claro y el texto oscuro, y la otra pondrá el fondo oscuro y el texto claro.
- Aplicaremos a nuestra página una clase u otra según la selección de la usuaria, apoyándonos en el `value` del input seleccionado.
- Paralelamente cada vez que la usuaria elija un tema, guardaremos esta información en `localStorage`.
- Al cargar la página buscaremos en `localStorage` el tema seleccionado en la última visita y lo aplicaremos sin que la usuaria tenga que realizar ninguna acción.

* * *

#### EJERCICIO 7

**Un formulario de verdad**

Vamos a seguir trabajando sobre el [ejercicio 4](#ejercicio-4). El formulario nos ha quedado un poco pobretón, añadamos al menos un campo más para el apellido.

¡Pero, ojo! Queremos tener nuestros datos agrupaditos. El reto es guardar y recoger del localStorage un objeto con dos propiedades, nombre y apellido.

¡A por ello!

* * *

#### EJERCICIO 8

Sobre el ejercicio 2 vamos a *cachear* las búsquedas al servidor. De forma que cuando a busquemos una cadena a través del campo de búsqueda, primero busque en localStorage si ya tenemos un resultado en local para esa cadena. Si no lo hay se pide al servidor y luego se guarda en `localStorage` usando como clave el texto de la búsqueda; si al buscarlo en `localStorage` lo encontramos pues le enseñamos el resultado directamente al usuario y nos evitamos una petición al servidor.

* * *

## Linter

Un linter es una herramienta que nos ayuda a prevenir errores y tener un formato homogéneo en nuestro código. Existen linters para varios lenguajes de programación, pero aquí veremos ESLint que es un linter para JavaScript.

En un linter definimos una serie de reglas en un fichero de configuración que son las que queremos comprobar en el código. Luego el programador que usa un linter ejecutará esas reglas, normalmente el propio editor (Code) lo hace por ti, y si no se cumplen te mostrará un error o un warning (aviso).

Hemos creado una configuración específica de linter para vosotras, Adalabers, porque queremos que os ayude a detectar algunos errores y a escribir código con un estilo correcto. Algunas de estas reglas son:
- da error si no se pone `;` al final de una sentencia
- da error si no se usa indentación correcta
- da warning si dejáis `console.log()` en el código
- da warning si dejáis una función vacía

Para usarlo en un proyecto, tenéis que
- descargar el fichero de configuración `.eslintrc.json` de [este repositorio](https://github.com/Adalab/linter-adalab)
- instalar ESLint de forma global mediante `npm install -g eslint`
- en el editor Code instalar el plugin `ESLint`.
- una vez configurado, al abrir un fichero JS nos aparecen los errores y warnings.
- En Code, si abrimos la paleta de comando (Ctrl + Shift + p) y escribimos `> ESLint`, nos aparecerán las opciones disponibles, una de ellas nos permite arreglar todos los errores solucionables.

A veces nos resultará molesto tener algunos errores o warnings en el editor porque, por ejemplo, queremos usar un `console.log` para algo. Podemos deshabilitar el uso del linter en una línea concreta usando [las instrucciones de configuración](https://eslint.org/docs/user-guide/configuring).

* * *

#### EJERCICIO 9

Para el proyecto anterior de la búsqueda en SWAPI, incluye el linter y corrige todos los errores detectados.

* * *

## BONUS

* * *

#### EJERCICIO 10 BONUS

**Dame gifs de gatetes**

Hay una api genial [thecatapi.com](https://thecatapi.com/docs.html) de imágenes de gatetes, como estos seres son muy particulares y no se juntan con cualquiera tenemos que autenticarnos siempre que hacemos una petición. Pero es una autenticación sencilla, solo tenemos que registrarnos en la web, y nos mandarán al email un *token* que nos identifica, y que tendremos que añadir en todas las peticiones que hagamos.

En Adalab ya nos hemos registrado y tenemos nuestro *token*. Te dejamos [un ejemplo](https://codepen.io/adalab/pen/YJVZGJ), a partir del cual hay que:

- Registrarse en la web y generar un token personal para sustituirlo por el de Adalab, que eso de impersonar a otros no es bonito.
- Pintar la imagen aleatoria del gato que nos devuelve la petición.
- ¡Espera! ¿Esto no iba de gifs? Vamos a ver si podemos hacer que la imagen que nos devuelve sea un gif.

> **Nota**: esta api es muy chachi, y una vez que nos autenticamos nos permite hacer cosas interesantes como guardar nuestras propias imágenes de gatetes, añadir a favoritos, eliminar nuestras imágenes... etc. Os animamos a leer la documentación y hacer diferentes pruebas con ella.

* * *

### Cazar errores del servidor

En la lección anterior vimos como gestionar errores con promesas, por otro lado en esta hemos visto las diferentes tipos de respuestas HTTP que nos puede devolver una llamada a un API. Veamos como combinar estos dos conceptos.

Cuando se resuelve la promesa de un fetch en esta nos llega información, uno de los datos es la propiedad `ok`. Esta es `true` si el código de respuesta es de tipo 200, en caso contrario es `false`. Una práctica extendida es cuando el valor de `ok` es falso generar una *excepción* con `throw`, ya que cuando hacemos esto dentro de un `then()` en lugar de ejecutarse el siguiente `then()` se ejecuta `catch()`. 

El API de Github nos devuelve un error cuando intentamos [pedir repositorios públicos](https://developer.github.com/v3/repos/#list-all-public-repositories) con un un valor no válido en el `queryParam` *since*. Veamos el ejemplo:

```js
fetch('https://api.github.com/repositories?since=asdf')
  .then(response => {
    if (!response.ok) {
      throw (response);
    }
    return response.json();
  })
  .then(data => console.log('success', data))
  .catch(err => console.log('error', err));
```

Puedes *trastear* este código:
- si arreglas el parámetro `since` de la url verás como se ejecuta el segundo `then()`
- si eliminas la excepción se ejecutará el segundo `then()` aunque el estado de la respuesta no sea de tipo 200.

## Resumen

En esta sesión hemos profundizado en el uso de las **APIs**, conocido el protocolo **HTTP** que estandariza la comunicación entre cliente y servidor en la web estableciendo un formato para los mensajes con la siguiente estructura:
- **Método HTTP** para las llamadas (POST, GET, PUT, PATCH, DELETE, OPTIONS...).
- **Código de respuesta** (1xx, 2xx, 3xx, 4xx, 5xx) para las respuestas.
- **Cabeceras** para incluir metadatos.
- **Cuerpo del mensaje**.

Pudiendo consultar todos estos datos para `debuggear` en la pestaña *Network* de las indispensables *DevTools* del navegador.

Como bonus podemos gestionar con `fetch` las respuestas con código diferente a 2xx, mediante la propiedad `ok` presente en la respuesta.

También hemos visto como **cachear** datos en el navegador de la usuaria gracias al uso de **localStorage**.

Y como las buenas prácticas marcan la diferencia, a partir de ahora tendremos un código homogéneo y con menos errores gracias al uso de un **linter**.

## Recursos externos

- [Listado de APIs pública](https://github.com/toddmotto/public-apis)
- [localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)
- [ESLint](https://eslint.org/)
