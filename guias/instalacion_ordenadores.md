# Instalación de ordenadores para el curso de Adalab

En el curso de programación front-end de Adalab necesitaremos usar un ordenador. Para poder realizar el curso de forma fluida, el ordenador debería tener estas características:

- Al menos 8GB de RAM (con 4GB irá algo más lento pero también se puede)
- Procesador i5 o similar con velocidad superior a 1GHz
- Disco duro: recomendamos desde 128GB; si es SSD va a ir más fluido que si es HDD pero se puede tener más capacidad por menos precio
- Tarjeta gráfica y pantalla: cualquiera pueden ir bien, aunque recomendamos pantalla de 15’ o como mínimo 13’ para poder programar junto a una compañera (con pantallas más pequeñas es posible pero se hace más complicado)

Para poder realizar el curso el sistema operativo (SO) del ordenador debe ser Linux o Mac, y no es posible realizarlo con Microsoft Windows. Si no tienes un Mac con OSX o un PC con Linux (recomendamos Ubuntu), en la siguiente sección te explicamos cómo instalarlo.

## Instalación de Ubuntu

En primer lugar, para los PCs que no tengan un sistema operativo Linux, recomendamos instalar Ubuntu. Tenemos 2 opciones:

- Instalar Ubuntu borrando todo lo que hay en el ordenador (recomendada): esta opción es obligatoria para equipos viejos que no tienen recursos para tener a la vez Windows y Linux
- Instalar Ubuntu junto a Windows: crearemos una partición del disco duro del ordenador para instalar Ubuntu, y luego poder arrancar el ordenador desde el SO que elijamos; esta opción es más compleja y depende del ordenador concreto que tengáis que pueda hacerse o no

> NOTA: Antes de proceder a la instalación es muy importante hacer una copia de seguridad de los datos que estén en el ordenador y que no queramos perder.

Usaremos la distribución de Ubuntu 18.04, que podemos descargar una ISO desde http://releases.ubuntu.com/18.04/ y grabaremos en un CD o pendrive. Un día antes de empezar el curso os ayudaremos a instalarlo y llevaremos pendrives preparados con esta versión. Seguiremos lo pasos de instalación para instalar y configurar el sistema.

Si queremos mantener Windows, tendremos que hacer una partición:

- Hacer partición siguiendo este tutorial: http://www.everydaylinuxuser.com/2015/11/how-to-shrink-windows-10-to-make-space.html
- Luego instalaremos Ubuntu así: http://dailylinuxuser.com/2015/11/how-to-install-ubuntu-linux-alongside.html

Además, puede que haya incompatibilidades de nuestro hardware (ordenador) con Ubuntu, [como esta que nos ha sucedido](https://plus.google.com/116778530198197186752/posts/baLJGdM52Wn
https://askubuntu.com/questions/38780/how-do-i-set-nomodeset-after-ive-already-installed-ubuntu
).

## Instalación de los programas

Una vez preparado el sistema, instalaremos algunos programas para el curso. En Ubuntu los podemos instalar con la interfaz visual (instalador de programas) o desde la terminal usando `apt-get install`. En Mac, recomendamos usar [homebrew](https://brew.sh/) para instalar desde la terminal.

Programas a instalar:

- git, versión 2.x (https://git-scm.com/downloads)
- nodejs, versión 10.x LTS (https://nodejs.org/en/)

Para comprobar que se ha instalado bien, ejecutar desde la terminal:

`node --version`

`git --version`

Desde el instalador visual, podremos instalar el resto (última versión de todos):

- VSCode (https://code.visualstudio.com/)
- Chrome (https://www.google.com/chrome/)
- Slack (https://slack.com/)

También usaremos cuentas en estos servicios:

- GitHub (https://github.com/)
- Trello (https://trello.com/)
