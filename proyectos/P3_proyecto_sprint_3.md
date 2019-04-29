# Proyecto 3: Un caso de código heredado

<!-- TOC START min:2 max:2 link:true update:true -->

- [Resumen (TL;DR)](#resumen-tldr)
- [Objetivos](#objetivos)
- [Caso de uso](#caso-de-uso)
- [Especificaciones](#especificaciones)
- [Planificación del proyecto](#planificacin-del-proyecto)
- [Entrega](#entrega)

<!-- TOC END -->

## Resumen ([TL;DR](https://spanish.stackexchange.com/questions/15317/hay-alg%C3%BAn-equivalente-en-castellano-al-ingl%C3%A9s-tldr))

En este proyecto vamos a trabajar con un caso muy típico que se suele producir en el mundo de la programación, un trabajo que nos viene dado, con código heredado, es decir escrito por otra persona y sobre el que tenemos que trabajar. En este caso es un poco especial porque vais a trabajar con código heredado pero vuestro: el código del proyecto del segundo módulo (el generador de tarjetas interactivas). **¡Sorpresa!**

## Objetivos

1. Lidiar con código heredado y ser capaces de refactorizarlo
2. Saber identificar y generar los componentes de una página, separarlos y crear componentes visualmente similares a partir de estos
3. Aprender a usar React para crear una aplicación web sencilla
4. Exponer en la sesión final y seguir adquiriendo habilidades de desarrollo personal
5. Aprender a buscar información en la documentación de librerías externas

## Caso de uso

La idea fundamental de este proyecto es que aprendamos a trabajar con un proyecto heredado. De esta forma desarrollaremos nuestra capacidad de adaptarnos a proyectos ya existentes. Esto nos preparará para, de cara al futuro, entrar en equipos nuevos de desarrollo con mayor rapidez, mejorar nuestra capacidad de modificación de código creado por otras personas y concienciarnos de la importancia de crear buen código visto desde la otra parte, la persona que lo recibe.

## Especificaciones

Se partirá de un proyecto funcional y se realizará una refactorización del código incluyendo el uso de React. _Refactorizar_ código consiste en modificar un código para mejorar su estructura pero sin añadir nuevas funcionalidades.

De cara a la refactorización, el proyecto debe utilizar estas tecnologías:

- Uso de Sass para los estilos
- Uso de ES6 y React para la estructuración del JS de la aplicación
- Uso de mediaqueries para que el diseño sea adaptable al dispositivo
- Desarrollo usando la estrategia mobile first
- Uso de git para el control de versiones del proyecto, con ramas y pull-requests para revisar los cambios de las compañeras
- Publicación del resultado en Internet usando GitHub Pages

La webapp deberá tener las siguientes nuevas características:

- Deberá usar transiciones y/o animaciones para mejorar interacciones con la aplicación

- Debe implementarse con una navegación entre distintas páginas de la aplicación usando React router

## Planificación del proyecto

### Sprints

Para la realización de este proyecto trabajaremos en _2 sprints_ (2 iteraciones) de 7 sesiones cada uno. Siguiendo los principios ágiles estableceremos pequeños ciclos iterativos de forma que al final de cada uno generemos valor perceptible por nuestros usuarios (los visitantes de la web). Dedicaremos el primer día a la planificación del sprint (_sprint planning_) y el resto a trabajar en el desarrollo del proyecto. Al final de cada sprint haremos una _demo_ del proyecto para presentar los resultados conseguidos, y una _retrospectiva_ (_retro_) para evaluar nuestro trabajo en equipo y mejorar en el siguiente sprint.

Al final del primer sprint haremos una demo corta de 5 minutos para presentar el resultado del trabajo al resto de las compañeras y a las profesoras. También haremos una retro corta revisando los _working agreements_ que hemos acordado al inicio del proyecto.

Al final del segundo sprint (final del proyecto), haremos una demo de 10 minutos con preguntas, y una retrospectiva usando una dinámica similar a las usadas en los equipos de desarrollo que usan SCRUM.

### Historias de usuario

Para la gestión del proyecto, usaremos _historias de usuario_, que es una herramienta para definir las características de un producto que veremos en detalle durante el curso. Usaremos las historias de usuario que ya tenemos definidas del proyecto anterior.

## Entrega

El formato de entrega de este proyecto será mediante la subida de este a la plataforma de GitHub. Para subirlo, se creará un repositorio en la organización de Adalab. El nombre del repositorio deberá estar compuesto de las siguientes partes, todo ello separado por guiones:

- Nombre de la promoción en minúsculas
- "m" minúscula seguida del número del módulo
- Nombre del equipo en minúsculas

Por ejemplo, el nombre de la primera promoción de Adalab fue "Ada". Si un grupo realizase un proyecto para el primer módulo y el nombre de ese grupo fuese "Lovelace", el nombre del repositorio debería ser "ada-m1-lovelace".

De manera adicional, se deberá activar "GitHub Pages" en el proyecto para que este pueda ser visualizado como una web, es decir, que en el caso anterior, si alguien introdujese la dirección "adalab.github.io/web-hopper/" en un navegador web, este mostraría la web que se genera con el código del repositorio.

## Presentación

El último día del módulo presentaréis la versión final de este proyecto a vuestras compañeras y al equipo de Adalab en el Meetup Space. Cada equipo realizará una presentación de 10 minutos y posteriormente habrá 10 minutos de feedback por parte del público.

Durante los días de feedback cada equipo tendrá asesoramiento durante 30 minutos sobre la presentación del proyecto grupal. Para aprovechar bien este espacio, es necesario que antes cada equipo haya decidido las cuestiones clave para la presentación.

A continuación algunos elementos que os pueden ayudar a enfocar la presentación:

- En el público habrá personas con conocimientos técnicos y no técnicos.
- El objetivo de la presentación es dar a conocer el producto creado, a las integrantes de cada equipo así como el proceso que habéis seguido para crear la web.
- Todas las participantes del equipo deben hablar en la presentación (sin práctica no hay mejora).

Otros elementos que podríais incluir (son solo ideas, sentíos libres de innovar y ser creativas):

- Presentación de las integrantes del equipo desde un punto de vista profesional: se tratar de practicar vuestro "relato" profesional en versión muy corta. Que las personas asistentes conozcan quienes sois como profesionales.
- Dejar muy claro quién ha sido vuestro cliente y qué fue lo que os pidió.
- Explicar qué necesidades cubre o qué problemas soluciona el producto, cuál es el beneficio principal que aporta y qué lo hace único comparado con otros productos parecidos del mercado.
- Os aconsejamos incluir una demo (ya sea mostrar la web online o hacer un vídeo).
- Aportaciones "únicas" de cada equipo al proyecto.
- La estructura del código y las partes que se quieran destacar.
- Cómo ha sido la organización del equipo, el reparto de tareas y la coordinación a la hora de trabajar todas en el mismo código.
- Cuál de las tareas o los puntos ha sido el que más esfuerzo ha requerido.
- Cuál de las tareas o partes de la web es la que hace que el equipo esté más orgulloso.
- La presentación debe tener un "buen cierre" que nos haga a todos aplaudir... ahí os dejamos que echéis a volar vuestra imaginación.
- No habléis en primera persona de lo que habéis hecho, hablad del equipo.
- No mencionéis problemas, sino "retos" que os han hecho aprender y crecer.
- Os aconsejamos utilizar un lenguaje ni demasiado formal y técnico, ni demasiado informal. Nuestra audiencia puede ser muy variada.

En este módulo os proponemos que de los diferentes elementos a incluir en la presentación os centréis un poco más en explicar las tecnologías y el código que habéis desarrollado.
