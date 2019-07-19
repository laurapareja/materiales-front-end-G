# Fases de maquetación de una página web

Hay muchas formas de afrontar la maquetación de una página web. Aquí proponemos una sencillita, con el objetivo de organizar mentalmente los pasos se pueden dar durante todo el proceso de maquetación. Cuando tengas experiencia maquetando lo harás a tu estilo y con los trucos que tú quieras, aquí solo proponemos una forma de trabajar.

Vamos empezar a organizar y escribir el código (HTML y CSS) de la página desde fuera (elementos más grandes) hacia dentro (elementos más pequeños). Debido a la herencia de CSS los estilos que damos a los elementos más grandes influyen en los de dentro.

A continuación detallamos cada uno de los pasos:

## Fases:

### 1: Añadir todos los contenidos

Empezamos añadiendo todos los contenidos de la página como: textos, listados, enlaces, imágenes...

### 2: Crear el esqueleto (o scaffolding)

Continuamos identificando aquellos elementos de la página web que componen un grupo, es decir, que actúan como una unidad. Sabemos que esos elementos (aunque sean muchos) se comportan como una unidad si:

* Se visualizan siempre juntos.
* Se visualizan en el mismo orden respecto a los elementos que les preceden y/o les siguen.
* Se visualizan en el mismo orden en todas las media queries.
* Se muestran y/u ocultan a la vez.
* Otras cosas dependiendo del diseño de la página.

### 3. Agrupar los elementos que forman un grupo o unidad

Tenemos que agrupar dentro de un contenedor (ya sea un `<div/>`, `<section />`, `<article />`... o cualquier otra etiqueta que nos sirva para agrupar) aquellos elementos que hemos identificado como un grupo o unidad.

Y debemos poner clases lo más descriptivas posibles a estos contenedores que hemos creado.

### 4. Maquetar el esqueleto

Una vez que hemos creado el esqueleto de la página vamos a empezar a maquetarlo. Para ello creamos nuestro fichero CSS y añadimos el siguiente código:

```css
* {
  box-sizing: border-box;
}

body {
  margin: 0;
}

/* sustituir los siguientes selectores por las clases de tus contenedores y añadir los que falten */
.header-container,
.main-container,
.footer-container {
  background-color: #eee;
  border: solid 5px #ccc;
}
```

Con este CSS conseguimos visualizar cada uno de los contenedores, ver qué espacio ocupan, cómo se distribuyen, dónde se colocan, cómo empujan a los contenedores qeu tienen alrededor...

Ahora ya podemos maquetar el esqueleto. Debemos crear los selectores que queramos y maquetar para distribuir estos contenedores o cajas para que se comporten como queremos.

Utilizaremos flexbox, grid, position... es decir, propiedades para distribuir y colocar los contenedores por la página.

El objetivo es ver que todos los contenedores se comportan como queremos. Si es necesario podemos darle un color de fondo diferente a cada contenedor.

> Nota: no debemos maquetar en esta fase los elementos internos de los contenedores. Por ello no nos tenemos que preocupar por tamaños de fuentes, colores, imágenes de background... Eso lo haremos en las siguientes fases.

<!-- ### 5. Separar el código en partials

Ya hemos dividido la página en sus diferentes partes o contenedores. Es el momento de dividir el código HTML en partials y el código CSS en partials de SASS.

Ya que estamos creando los partials de SASS, es un buen momento para crear otros partials como por ejemplo el de variables y reset.

Al finalizar tendremos nuestro código muy limpio y ordenado. Nuestra mente entrará en modo zen ;) -->

## Durante todo el proceso de maquetación

Durante todo el proceso de maquetación tenemos que seguir las siguientes pautas:

* Indentamos desde el primer momento. Identar no es solo para que el código quede legible. También para que durante la programación veamos que no estamos cometiendo ningún error.
* Los textos de la página debemos escribirlos en el HTML de forma gramáticalmente correcta, como nos enseñaron en el colegio. Si en los diseños el título principal es "BIENVIENDA A ADALAB", en el código hay que poner "Bienvenida a Adalab". Y para ponerlo en mayúsculas utilizaremos propiedades de CSS.
* Los nombres de las clases tienen que describir lo que son.
* Evitamos los nombres de clases con números. Por ejemplo, no nos gusta usar las clases `.title1` y `.title2`. Preferimos `.title` y `.subtitle`.
* Una etiqueta por renglón para ayudar a la legibilidad del código. Por ejemplo:

```html
<!-- esto no es legible -->
<ul class="list"><li class="link"><a href="http://adalab.es" class="link">Adalab</a></li></ul>

<!-- esto se lee muy fácilmente -->
<ul class="list">
  <li class="item">
    <a href="http://adalab.es" class="link">Adalab</a>
  </li>
</ul>
```