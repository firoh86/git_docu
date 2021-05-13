Comprendiendo/Aprendiendo GIT

Los términos que vamos a cubrir en esta documentación serán:

git clone, git config, git add, git status, git commit, git push, git pull, git branch, git checkout, git merge.

-¿Qué es GIT?

Es el sistema de control de versiones más extendido y moderno a día de hoy a nivel mundial.
Git está desarrollado y es un proyecto de código abierto activamente mantenido y desarrollado en 2005 por Linus Torvalds. El famoso creador de Linus y los sistemas operativos basados en kernel.

-Preparando un repositorio.

git init/ git clone/ git config

Inicializando un nuevo repositorio GIT

Pra crear un nuevo repositorio, usarás el comando git init.
git init es un comando que usaras una vez durante la creacion inicial del repositorio.
Ejecutando este comando, se creara un subdirectorio nuevo .git en la dirección actual, esto además creará yna nueva master branch.

-Versionando un proyecto existente con un nuevo repositorio git.

Este ejemplo asume que ya tienes una carpera con un proyecto existente para el que te gustaría crear un repositorio.
Este ejemplo asume que ya tienes una carpera con un proyecto existente para el que te gustaría crear un repositorio. Lo primero que deberías hacer es ir a la ruta raiz del proyecto para ejecutar el git init.

Se puede realizar de dos maneras, llendo a la ruta y ejecutando git init ó ejecutando git init y pasando la ruta como parametro git <project directory>

-Clonando un repositorio existente.
Git clone

Si el proyecto ya ha sido creado como un repositorio central, el comando de git clone, es la forma comúnmente más usada para obtener un clone de desarrollo local.
Al igual que Git init, git clone es una operación de un solo uso, una vez que el desarrollador ha obtenido una copia funcional del proyecto, todas las operaciones de control de versiones, serán manejadas a través del repositorio local.

git clone <repo url>

Git soporta diferentes protocolos de conexión y formatos de URLs.
En este ejemplo estaremos usando el protocolo SSH
por ejemplo: git@HOSTNAME:USERNAME/REPONAME.git

Los valores dados en éste caso serían los siguientes:

HOSTNAME: bitbucket.org

USERNAME:rhyolight

REPONAME: javascript-data-store

Cuando lo ejecutes, la última versión de los archivos del repositorio en la rama master serán descargadas y añadidas a una carpeta nueva.
La carpeta será renombrada con el nombre del repo.
Esta carpeta, además de los archivos del repositorio tendrá la historia completa de modificaciónes de versión del repositorio original, además se creará una rama maestra local.

-Git Add

El comando de git add añade los cambios de la carpeta en que estemos trabajando a supervisión. git add realmente no causa modificaciónes la repositorio hasta que hacemos el git commit.

En conjunción con esos comandos, necesitarás además git status para ver en que estado se encuentra la supervisión.
(Se muestran los archivos con seguimiento que se tendrán en cuenta para el siguiente commit).

-Cómo funciona:
git add y git commit son comandos que componen el flujo de trabajo fundamental de git.
Esos son dos comandos que todo usuario de git debe comprender. Indiferentemente del flujo de trabajo de su equipo de desarrollo.
Son los medios para registrar versiones de un proyecto en el historial del repo.

En adición con git add y git commit el comando git push es esencial para un flujo de trabajo colaborativo completo. Git push es usado para enviar los cambios guardados a un repositorio remoto. Esto permite a otro miembros del equipo tener acceso al conjunto de cambios guardados.
cambios para comitear

-Guardando cambios al repositorio
git commit

convención para los commits
https://www.conventionalcommits.org/es/v1.0.0-beta.2/#especificaci%c3%b3n

Una vez que tienes un repositorio inicializado o clonado, ya puedes empezar a hacer commits de los cambios de los archivos.(toma un snapshoot del estado actual de los archivos que han sido modificados).
El siguiente ejemplo asume que tienes un repositorio inicializado en:
/path/to/project.

ir al root del repositorio.
creamos un nuevo archivo file.txt
usamos el comando git add para añadir el archivo a supervisión.
Usamos git commit para comitear los archivos previamente añadidos a supervision.
Comentamos el commit para añdir información de lo que hemos añadido en esta nueva versión.
git commit -m "added where are the changes & what they do".
