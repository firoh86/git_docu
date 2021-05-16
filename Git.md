# Comprendiendo / Aprendiendo GIT

Los términos que vamos a cubrir en esta documentación serán:

- [¿Qué es GIT?](#que-es-git)
- [Preparando un repositorio](#preparando-un-repositorio)
- [Versionando un proyecto existente](#versionando-un-proyecto-existente-con-un-nuevo-repositorio-git)
- [Comandos GIT](#comandos)

  - [git clone](#git-clone)
  - [git add](#git-add)
  - [git commit](#git-commit)
  - [git diff](#git-diff)
  - [git stash](#git-stash)
  - [gitignore](#gitignore)
  - [git status](#git-status)
  - [git log](#git-log)

  - git config
  - git push
  - git pull
  - git branch
  - git checkout
  - git merge

---

## ¿Qué es GIT?

Es el sistema de control de versiones más extendido y moderno a día de hoy a nivel mundial.
Git está desarrollado y es un proyecto de código abierto activamente mantenido y desarrollado en 2005 por Linus Torvalds. El famoso creador de Linux y los sistemas operativos basados en kernel.

--- 

## Preparando un repositorio

**git init/ git clone/ git config**

Inicializando un nuevo repositorio GIT.

Para crear un nuevo repositorio, usarás el comando `git init`.
*git init* es un comando que usarás una vez durante la creación inicial del repositorio.
Ejecutando este comando, se creará un subdirectorio nuevo .git en la dirección actual, esto además creará una nueva master branch.

---

## Versionando un proyecto existente con un nuevo repositorio git

Este ejemplo asume que ya tienes una carpeta con un proyecto existente para el que te gustaría crear un repositorio. Lo primero que deberías hacer es ir a la ruta raiz del proyecto para ejecutar el git init.

Se puede realizar de dos maneras, yendo a la ruta y ejecutando `git init` ó ejecutando git init y pasando la ruta como parámetro `git <project directory>`

---

## Comandos

## Git clone
### Clonando un repositorio existente


Si el proyecto ya ha sido creado como un repositorio central, el comando de *git clone*, es la forma comúnmente más usada para obtener un clone de desarrollo local.
Al igual que git init, *git clone es una operación de un solo uso*, una vez que el desarrollador ha obtenido una copia funcional del proyecto, todas las operaciones de control de versiones, serán manejadas a través del repositorio local.


`git clone <repo url>`


Git soporta diferentes protocolos de conexión y formatos de URLs.
En este ejemplo estaremos usando el protocolo SSH
por ejemplo: **git@HOSTNAME:USERNAME/REPONAME.git**

Los valores dados en éste caso serían los siguientes:
```
HOSTNAME: bitbucket.org

USERNAME:rhyolight

REPONAME: javascript-data-store
```

Cuando lo ejecutes, la última versión de los archivos del repositorio en la rama master serán descargadas y añadidas a una carpeta nueva.
La carpeta será renombrada con el nombre del repo.
Esta carpeta, además de los archivos del repositorio tendrá la historia completa de modificaciónes de versión del repositorio original, además se creará una rama maestra local.

---

## Git add

El comando de `git add` añade los cambios de la carpeta en que estemos trabajando a supervisión. git add realmente no causa modificaciones al repositorio hasta que hacemos el git commit.

En conjunción con esos comandos, necesitarás además git status para ver en que estado se encuentra la supervisión.
(Se muestran los archivos con seguimiento que se tendrán en cuenta para el siguiente commit).

### Cómo funciona:
`git add y git commit` son comandos que componen el flujo de trabajo fundamental de git.
Estos son dos comandos que todo usuario de git debe comprender. Indiferentemente del flujo de trabajo de su equipo de desarrollo.
***Son los medios para registrar versiones de un proyecto en el historial del repo.***

En adición con git add y git commit el comando `git push` es esencial para un flujo de trabajo colaborativo completo. `Git push` es usado para enviar los cambios guardados a un repositorio remoto. Esto permite a otro miembros del equipo tener acceso al conjunto de cambios guardados.

### Los archivos supervisados

En lugar de commitear cada cambio que has hecho desde el último commit, la supervisión te permite agrupar cambios relacionados antes de comitearlos en la historia del proyecto. Esto significa que puedes hacer todo tipo de edición para agrupar archivos relacionados antes de hacer un commit.
Es importante crear commits atómicos que hagan más fácil el seguimiento de bugs para revertir los cambios con el menor impacto posible.

-Opciones comunes:

`git add <file>`
Añade a supervisión los cambios de los archivos nombrados

`git add <directory>`
Añade a supervisión los cambios de las carpetas nombradas.

`git add .`
Añade todos los cambios desde la raiz del bash.

`git add -p`
Añade un bloque de los cambios realizados en un archivo, esto te permite de forma manual controlar los cambios en un mensaje de la consola.
Para el bloque de cambios
`y` para aceptar el bloque de cambios
`s` para partir el bloque en partes más pequeñas
`e` para editar el bloque manualmente
`q` para salir

### Relación entre git add y git commit

Cuando empiezas un proyecto puedes crear un commit para el estado inicial en ese directorio, usando ambos comandos juntos asi:

```
git add . git commit
```
Una vez que estás corriendo el proyecto, los nuevos archivos pueden ser añadidos y pasados al path de git add:
```
git add hello.py git commit
```

***git no diferencia entre archivos supervisados en archivos y archivos nuevos que acaban de ser añadidos al repositorio.***

---


## Git commit

### Guardando cambios al repositorio

[Ver convención para los commits](
https://www.conventionalcommits.org/es/v1.0.0-beta.2/#especificaci%c3%b3n)

Una vez que tienes un repositorio inicializado o clonado, ya puedes empezar a hacer commits de los cambios de los archivos.(toma un snapshot del estado actual de los archivos que han sido modificados).
El siguiente ejemplo asume que tienes un repositorio inicializado en:
`/path/to/project.`

-Ir al root del repositorio.
-Creamos un nuevo archivo file.txt
-Usamos el comando `git add` para añadir el archivo a supervisión.
-Usamos `git commit` para comitear los archivos previamente añadidos a supervision.
-Comentamos el commit para añadir información de lo que hemos añadido en esta nueva versión.
```
git commit -m "added where are the changes & what they do".
```

---

## Git diff

Diferenciar es una función que toma dos datos de entrada y devuelve los cambios entre éstos.
`git diff` es un comando de uso múltiple.
Estos datos diferenciales pueden ser comiteados, podemos crear ramas a partir de ellos, archivos y más.
Vamos a ver los diferentes patrones de flujo de trabajo con git diff.
`git diff` es comúnmente usado a su vez con `git status` y `git log` para analizar el estado actual de un repositorio.

### Información de salida raw
El siguiente ejemplo se ejecuta en un repositorio simple.
El repo ha sido creado con éstos comandos:
```
$:> mkdir diff_test_repo
$:> cd diff_test_repo
$:> touch diff_test.txt
$:> echo "this is a git diff test example" > diff_test.txt
$:> git init .
Initialized empty Git repository in /Users/kev/code/test/.git/
$:> git add diff_test.txt
$:> git commit -am"add diff test file"
[master (root-commit) 6f77fc3] add diff test file
1 file changed, 1 insertion(+)
create mode 100644 diff_test.txt
```
Si ejecutamos el `git diff` en este punto, no habrá salida, esto es un comportamiento esperado cuando no hay cambios en el repositorio para diferenciar.

Una vez que hemos creado el repositorio y añadido el archivo diff_test.txt podemos cambiar el contenido del archivo para experimentar con la salida de git diff.

```
$:> echo "this is a diff example" > diff_test.txt
```
Con esto modificamos el contenido desde bash del archivo diff_test.txt
Ahora podremos ver y analizar los cambios con git diff:
```
diff --git a/diff_test.txt b/diff_test.txt
index 6b0c6cf..b37e70a 100644
--- a/diff_test.txt
+++ b/diff_test.txt
@@ -1 +1 @@
-this is a git diff test example
+this is a diff example
```

Vamos a analizar esta salida por puntos

### Comparison input
```
diff --git a/diff_test.txt b/diff_test.txt
```
Aquí podemos ver un a diff_text y un b diff_test

### Meta data
```
index 6b0c6cf..b37e70a 100644
```

Esta línea muestra alguna info interna de Git, normalmente no necesitarás esta info.
El número corresponde con el hash de versión del objeto en git

### Marcadores para cambios
```
--- a/diff_test.txt
+++ b/diff_test.txt
```

Estas líneas son leyendas asignadas a cada entrada del diff con --- en a y +++ en b

### Diff bloques
La salida del diff que nos queda es una lista de bloques, el diff solo muestra las secciones del archivos que han sido modificadas.
En nuestro ejemplo, solo contamos con un bloque, los bloques tienen su propia semántica de salida

```
@@ -1 +1 @@
--- a/diff_test.txt
+++ b/diff_test.txt
```

La primera línea es la cabecera del bloque, cada bloque pretende ser encapsulado entre simbolos de @@. El contenido de la cabecera es un sumario de los cambios realizados en el archivo. En nuestro ejemplo de salida tenemos -1 y +1 significando que una línea ha cambiado. En un diff más realista nosotros podríamos ver una cabecera más parecida a ésta:
```
@@ -34,6 +34,8 @@
```
En este ejemplo, el header nos muestra que han sido extraidas 6 líneas empezando en la línea 34 y adicionalmente 8 líneas han sido
añadidas empezando en la línea 34

### Resaltando cambios
```
git diff --color-words
```
`git diff` además tiene un modo para resaltar los cambios de una mejor manera: `--color-words`. Este modo simplemente crea un resalte de color entre las líneas agregadas y borradas y luego las resalta para diferenciarlas.

- Comparando archivos entre dos commits diferentes
A `git diff` le puedes pasar referencias de dos commits para diferenciar, ejemplos de referencias son head, etiquetas y nombres de ramas.
Cada commit en Git tiene un ID. Puedes conseguirlos ejecutando `git log`. También puedes pasar este commit id a git diff:

  Pasando una ref diff con estado actual
  Pasando dos reds diff entre ambos estados.

- Comprobando los cambios entre dos ramas.

  Las ramas son comparadas del mísmo modo como si estuviesemos comparando dos commits, pasandole los inputs:

```
git diff branch1..other-feature-branch
```

Este ejemplo introduce el operador de puntos suspensivos.
Los dos puntos en este ejemplo indican que son las puntas de ambas ramas. Esto funciona igual si intercambiamos el operador de dos puntos por un espacio entre las ramas.

```
git diff branch1...other-feature-branch
```

El operador de tres puntos nos mostrará las diferencias entre la rama de referencia y la rama master desde que éstas se separaron.

--- 

## Git stash

`git stash` nos permite crear una copia de nuestro trabajo no comiteado para movernos a trabajar en otra cosa como otra rama, otro feature manteniendo una copia de nuestro trabajo en el estado actual.Para poder volver después y seguir trabajando con ello.

Los comandos son:

`git stash`, copia los archivos stageados y trackeados.
`git stash -u` copia además los archivos no trackeados.
`git stash -a` copia todos los archivos, incluyendo también los archivos ignorados (gitignore).

***Hay que tener en cuenta que por defecto git stash no incluye los archivos no trackeados o ignorados.***

Para reaplicar los cambios de tu stash a tu rama actual lo hacemos con el comando:
`git stash pop`
(git stash pop aplica los cambios guardados en el stash y los borra del stash).

Para reaplicar los cambios a tu rama actual manteniendo la copia del stash lo podemos hacer con el comando:
`git stash apply`
(De esta manera pese a aplicar los cambios, los mantenemos en el stash para trabajar con ellos más tarde o en otra rama si nos fuese necesario).

### Manejando múltiples stashes

Podemos crear tantos stashes como queramos para trabajar con ellos.
Sería una buena práctica anotar una descripción para cuando trabajamos con múltiples copias del stash, podemos hacerlo de esta manera:

`git stash save "message"`

Para ver la lista de copias creadas con el stash lo podemos hacer con:

`git stash list`

Los stashes se muestran con la cabecera de la rama y el commit o mensaje guardado de esta manera.
```
$ git stash list
stash@{0}: WIP on master: 5002d47 our new homepage
stash@{1}: WIP on master: 5002d47 our new homepage
stash@{2}: WIP on master: 5002d47 our new homepage
```
Por defecto `git stash pop` aplicará los cambios del stash más recientemente creado.
Puedes elegir que stash quieres reaplicar pasándole el identificador como argumento, por ejemplo:

`git stash pop stash@{2}`

### Viendo las stash diffs

Puedes ver un sumario de diferencias de un stash con *git stash show*:

`$ git stash show`
```
index.html | 1 +
style.css | 3 +++
2 files changed, 4 insertions(+)
```

O también puedes ver una lista completa de las diferencias del stash pasándole el parametro `-p` ó `--path`

`$ git stash show -p`
```
diff --git a/style.css b/style.css
new file mode 100644
index 0000000..d92368b
--- /dev/null
+++ b/style.css
@@ -0,0 +1,3 @@
+\* {

- text-decoration: blink;
  +}
  diff --git a/index.html b/index.html
  index 9daeafb..ebdcbd2 100644
  --- a/index.html
  +++ b/index.html
  @@ -1 +1,2 @@ +<link rel="stylesheet" href="style.css"/>
```

### Partial stashes

Puedes elegir para stashear un archivo único, una colección de archivos o cambios individuales de entre los archivos. Si le pasas el parámetro `-p` o `--patch` a git stash, integrará integrará un bloque entre cada cambio en tu copia de trabajo y te preguntará donde quieres stashearlo.

Si pulsas `git stash ?` te aparece una lista más completa de comandos que puedes utilizar

### Creando una rama para nuestro stash

Si los cambios de tu rama divergen de los cambios en tu stash, puedes tener algunos conflictos cuando quieras hacer `git stash pop` o `git stash apply`, para evitar estos conflictos, quizás prefieras crear una rama para los cambios del stash, puedes hacerlo utilizando para ello:

`git stash branch`

Nuestra nueva rama estará basada en el commit de la que fue creada, entonces hará un pop de tus cambios stasheados en ella.

### Limpiando el stash

Si decides que ya no necesitas un stash en particular, puedes borrarlo con git stash drop:

`git stash drop stash@{1}`

O podrías borrar todos los stashes almacenados con:

`git stash clear`

---
## Gitignore

Git tiene 3 formas de ver los archivos de tu copia de trabajo:
Archivos trackeados, sin trackear o ignorados.

Los archivos ignorados son artefactos de la creación de un proyecto o generados por la máquina y pueden ser derivados del código de tu repo o deberían de otro modo no ser comiteados. Algunos ejemplos son:

cachés de dependencias, código compilado, código compilado, directorios de salida de builds, archivos generados en tiempo de ejecución, archivos ocultos de sistema, o configuraciones personales del IDE.

Los archivos ignorados son trackeados en especial el gitignore, que es comprobado en la raiz del repositorio.
Este archivo solo puede ser añadido o comiteado manualmente, y en él especificamos que archivos de nuestro queremos que sea o no ignorado.

---
## Git status

#### Inspeccionando un repositorio

El comando git status muestra un estado del directorio de trabajo y su estado actual, te deja ver los cambios que han sido stageados, los que no y los archivos que no han sido trackeados.
Git status no proporciona ningún tipo de información de salida como el historial de los commits, para esto necesitamos usar git log.

Comandos relacionados a git status:

`git tag`
Los tags son referencias de puntos especificos en la historia de git.
Generalmente son usados para capturar un punto en la historia como podría una versión de release (ver 1.0).

`git blame`
La función principal de git blame es mostrar la información del autor unida a un lineas especificas de un archivo o un archivo en sí. Es usado para extraer información de quien o porque modificaron x archivo o lineas de código.
ejemplos:
```
git blame filename
git blame filename -L 0,10
```
---
## Git log

**git log** muestra una lista de los commits realizados en el repositorio. Esto te permite listar la historia del proyecto, filtrarla o buscar cambios especificos.

La salida de este comando puede ser definida de diferentes formas para recibir un historial más especifico para el caso que estemos buscando.

`git log`

`git log -n <limit>`
Limita el número de commits por, por ejemplo: git log -n 3 mostrará solo 3 commits desde el más actual.

`git log --oneline`
Condensa cada commit en una línea única, es útil para ver una vista más global de la historia del proyecto.

`git log --stat`
Además de la información ordinaria de git log, incluye que archivos fueron alterados y el número relativo de líneas que fueron añadidas o borradas de cada uno de ellos.

`git log -p`
Muestra la ruta representada en cada commit, muestra el diff completo en cada commit, el cual es una vista más detallada que puedes tener en la historia de tu proyecto.

`git log --author="<pattern>"`
Busca los commits de un autor en particular. El parámetro puede ser un texto plano o una expresión regular.

`git log --grep="<pattern>"`
Busca commits con un mensaje que coincida, el cual puede ser texto plano o expresión regular.

`git log <since>..<until>`
Muestra los commits que vas desde since hasta until, ambos argumentos pueden ser también un commitID, en nombre de una rama, una cabecera, o algún tipo de referencia de revisión.

`git log <file>`
Solo muestra los commits que incluyen un archivo especifico, es una forma fácil de ver la historia de un archivo en particular.

`git log --graph --decorate --oneline`
Una opción bastante útil a considerar. El flag de --graph dibujará a la izquierda basado en texto un gráfico de los commits. --decorate añade los nombres de las ramas y tags de los commits que son mostrados.--oneline condensa la info de los commits en una sola línea para que sea más fácil navegar entre ellos.
