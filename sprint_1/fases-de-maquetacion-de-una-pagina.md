# Fases de maquetación de una página web

Hay muchas formas de afrontar la maquetación de una página web. Aquí proponemos una sencillita, con el objetivo de organizar mentalmente los pasos se pueden dar durante todo el proceso de maquetación. Cuando tengas experiencia maquetando seguirás tus propias fases.

Vamos empezar a organizar y escribir el código (HTML y CSS) de la página desde fuera (elementos más grandes) hacia dentro (elementos más pequeños). Debido a la herencia de CSS los estilos que damos a los elementos más grandes influyen en los de dentro.

A continuación detallamos cada uno de los pasos:

### 1: Añadir todos los contenidos

Empezamos añadiendo todos los contenidos de la página como: textos, listados, enlaces, imágenes...

### 2: Crear el esqueleto (o scaffolding)

Continuamos identificando aquellos elementos de la página web que componen un grupo, es decir, que actúan como una unidad. Sabemos que esos elementos (aunque sean muchos) se comportan como una unidad si:

* Se visualizan siempre juntos.
* Se visualizan en el mismo orden respecto a los elementos que les preceden y/o les siguen.
* Se visualizan en el mismo orden en todas las media queries.
* Se muestran y/u ocultan a la vez.
* Otras cosas dependiendo del diseño de la página.

## 3. Agrupar los elementos que forman un grupo o unidad

Tenemos que agrupar dentro de un contenedor (ya sea un `<div/>`, `<section />`, `<article />`... o cualquier otra etiqueta que nos sirva para agrupar) aquellos elementos que hemos identificado como un grupo o unidad.

Y debemos poner clases lo más descriptivas posibles a estos contenedores que hemos creado.
