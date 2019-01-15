# Lifting

[codepen-lifting-events]: https://codepen.io/adalab/pen/wpmyjB?editors=0010

## Contenidos

<!-- TOC -->

- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)
- [EJERCICIO 3](#ejercicio-3)

<!-- /TOC -->

## Introducción

Hemos visto que los eventos nos permiten declarar qué reacciones tendrán nuestros componentes. Sin embargo, en ocasiones necesitamos que una reacción en un componente hijo/a, como puede ser la que causa un evento, provoque una reacción en el elemento padre/madre, o incluso más arriba en la cadena.

React solo nos permite pasar datos unidireccionalmente, de padres/madres a hijos/hijas. Aunque esto puede parecer una limitación, debemos recordar que las funciones en JavaScript se tratan como datos, podemos guardarlas en variables, y conservan las variables del ámbito donde se declararon. Así que, ¿y si declarásemos una función en el padre/madre que provoque una reacción en el propio componente y se la pasamos como `prop` a un hijo/a? Eso es una **práctica habitual en React** que se llama _lifting_, que significa "alzamiento".

## ¿Para qué sirve lo que vamos a ver en esta sesión?

Para poder pasar información desde cualquier componente a cualquier otro componente de nuestra aplicación de React.

## _Lifting_ (alzamiento) para pasar datos de hijos a padres

_Lifting_ es una técnica que consiste en pasar funciones a los hijos/as y que sean estos quienes se encarguen de ejecutarlas cuando sea necesario, provocando un cambio _hacia arriba_, en los padres. Generalmente se usa para cambiar el _estado_ de los padres, que luego provocará un re-`render`izado de los hijos/as con nuevas `props`.

Vamos a ver un ejemplo, con Murrays de nuevo. Tenemos tres componentes, `MurrayList`, `RandomMurray` y `ReloadButton`, cada uno en su módulo. `MurrayList` renderiza una lista con varios componentes `RandomMurray`, y además un botón `ReloadButton`.

**components/MurrayList.js**

```js
import React from 'react';
import RandomMurray from `./RandomMurray`;
import ReloadButton from './ReloadButton';

class MurrayList extends React.Component {
  constructor(props) {
    super(props);

    // nos aseguramos de que este callback se ejecute siempre sobre el componente enlazándolo a la instancia con "bind"
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.forceUpdate(); // se ejecutará el método `render()` de MurrayList, que hará a su vez que se ejecute de nuevo el método `render()` de los hijos
  }

  render() {
    const { handleClick } = this;

    return (
      <section className="section-murrays">
        <h1>All <del>Cats</del> Murrays Are Beautiful</h1>
        <ul className="section-murrays_list">
          <li><RandomMurray /></li>
          <li><RandomMurray /></li>
          <li><RandomMurray /></li>
        </ul>
        {/* pasamos handleClick al hijo como prop */}
        <ReloadButton actionToPerform={ handleClick } label="More murrays"/>
      </section>
    );
  }
}

export default MurrayList;
```

Como vemos en el componente `MurrayList` llamamos a un componente `ReloadButton` al que pasamos por `props` una función que llamamos `actionToPerform`. Esta prop apunta a al método `handleClick` que simplemente hace un forceUpdate que provoca una llamada al render y por tanto el re-renderizado de todas las hijas, las 3 `RandomMurray`, provocando el pintado de 3 nuevas imágenes aleatorias.

**components/ReloadButton.js**

```js
import React from "react";

class ReloadButton extends React.Component {
  render() {
    const { label = "More", actionToPerform } = this.props;

    return (
      // Registramos el escuchador que recibimos por props. ¡Lifting hecho!
      <button onClick={actionToPerform}>{label}</button>
    );
  }
}

export default ReloadButton;
```

En `ReloadButton` es donde sucede el _lifting_: recogemos la función que llega de la madre por props (`actionToPerform`) y se la asignamos al `onClick` del botón. De esta forma, al hacer click en el botón ejecutamos una función de la madre.

**components/RandomMurray.js**

```js
import React from "react";

const getRandomInteger = (max, min) =>
  Math.floor(Math.random() * (max - min + 1)) + min;
const MIN_SIZE = 200;
const MAX_SIZE = 400;

class RandomMurray extends React.Component {
  render() {
    const randomMurray = getRandomInteger(MIN_SIZE, MAX_SIZE);

    return (
      <img
        src={`http://loremmurray.com/400/200/${randomMurray}`}
        alt="Random murray"
      />
    );
  }
}

export default RandomMurray;
```

**index.js**

```js
import React from "react";
import ReactDOM from "react-dom";
import "./stylesheets/index.css";
import MurrayList from "./components/MurrayList";

ReactDOM.render(<MurrayList />, document.getElementById("react-root"));
```

&blacktriangleright; [_Lifting_ de eventos en Codepen][codepen-lifting-events]

---

#### EJERCICIO 1

**Ciudades**

Para terminar de entender bien cómo funciona el lifting vamos a hacer un ejercicio muy sencillo. Partimos de un select con nombre de ciudades que encapsulamos en un componente `CitySelector`. Vamos a hacer que, al seleccionar una ciudad del select, aparezca una foto de la misma al lado. La diferencia con ejercicios anteriores es que ahora el select está en su propio componente, y debemos usar lifting.

---

#### EJERCICIO 2 

**Traductor MIMIMI**

¿No os ha pasado nunca que habéis dicho algo y se han burlado de vosotras con un MIMIMI?

- "Al final de esa línea te falta un punto y coma."

- "Il finil di isi linii ti filti in pinti y cimi."

Pues es hora de contraatacar y crear nuestro propio traductor MIMIMI con React.

Vamos a partir de un formulario simple con un textarea donde escribimos una frase. Según vamos escribiendo, obtendremos en un párrafo el resultado de la traducción a MIMIMI. Es importante que tanto formulario como el párrafo resultado estén cada uno en su propio componente independiente. El componente del formulario, por ejemplo `TextInput`, simplemente se encarga de recoger los cambios de la usuaria y enviarlo al componente madre `App`, que los guarda en su estado. El componente `MIMIMITranslator` recoge el texto que le pasan por props, lo traduce y muestra en un párrafo.

> PISTA: para realizar la traducción basta con buscar [una expresión regular (RegExp)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp) y el método `replace` de las cadenas. Si buscas "javascript regex replace vowels" en Google va a ser fácil de encontrar.

---

#### EJERCICIO 3

**Filtrando artículos**

Vamos a partir del ejercicio 1 de la sesión 3.5 (los items de la lista de la compra). Si recuerdas bien, teníamos un componente `ItemList` que mostraba un listado de `Item`s. Vamos a crear un nuevo componente `CategoryButton` que es un botón con el nombre de una categoría de productos y que recibe por `props` el nombre de la categoría.

```html
<CategoryButton category="Bebida" />
```

En nuestro `ItemList` vamos a pintar, además del `ul` con el listado de items, un botón con una categoría, por ejemplo, 'Bebida'.

> Recuerda que un componente de React sólo debe tener un elemento raíz en su método `render` y si queremos meter más cosas debemos agruparlas, por ejemplo, en un `div`.

Ahora viene lo bueno: vamos a escuchar eventos `click` sobre el botón de la categoría, de forma que se invoca un método del componente madre (`ItemList`) que hemos recibido por `props` (_lifting_). A este método de la madre le pasamos como parámetro el nombre de la categoría, para que sepa qué botón se ha clicado. Ya en `ItemList` definimos ese método para que si se pulsa el botón de la categoría bebidas sólo aparezcan los items de esa categoría en pantalla. Esto podemos hacerlo de varias formas:

- si tenemos todos los items en un array, podemos filtrarlos con `filter` para dejar solo los de la categoría seleccionada
- podemos pasar una prop más a los `Item` para indicar si está visible o no, y ocultarlo con una clase CSS

Al final, elijamos la que elijamos, tendremos que realizar un cambio de estado para forzar la ejecución del método `render` de `ItemList` que a su vez fuerza el de sus hijas.

_BONUS_: cuando tenemos todo funcionando para una categoría, podemos añadir botones para cada de las que tengamos productos. Incluso un botón especial 'Todos' para mostrar de nuevo los productos de todas las categorías.

---

## Recursos externos

### Documentación oficial de facebook sobre lifting

- [Lifting State Up](https://reactjs.org/docs/lifting-state-up.html)

- [JavaScript Regular Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)
