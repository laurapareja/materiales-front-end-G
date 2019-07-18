# Fases de maquetación de una página web

A continuación se detallan las fases de maquetación de una página web.

Vamos empezar a organizar y escribir el código (HTML y CSS) de la página desde fuera (elementos más grandes) hacia dentro (elementos más pequeños). Debido a la herencia de CSS los estilos que damos a los elementos más grandes influyen en los de dentro.

1. Añadir todos los contenidos (textos, listados, enlaces, imágenes).
2. Crear el esqueleto (o scaffolding):
   1. Hay que identificar aquellos elementos de la página web que componen un grupo, es decir, que actuan como una unidad. Sabemos que esos elementos (aunque sean muchos) se comportan como una unidad si:
      * Se visualizan siempre juntos.
      * Se visualizan en el mismo orden respecto a los elementos que les preceden y/o les siguen.
      * Se visualizan en el mismo orden en todas las media queries.
      * Se muestran y/u ocultan a la vez.
    2. Agrupamos los elementos que forman un grupo o unidad dentro de un contenedor (ya sea un `<div/>`, `<section />`, `<article />`... o cualquier otra etiqueta que nos sirva para agrupar).
    3. Ponemos clases lo más descriptivas posibles a los contenedores que hemos creado.
3. Continuará...