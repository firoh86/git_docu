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
_git init_ es un comando que usarás una vez durante la creación inicial del repositorio.
Ejecutando este comando, se creará un subdirectorio nuevo .git en la dirección actual, esto además creará una nueva master branch.

---

## Versionando un proyecto existente con un nuevo repositorio git

Este ejemplo asume que ya tienes una carpeta con un proyecto existente para el que te gustaría crear un repositorio. Lo primero que deberías hacer es ir a la ruta raiz del proyecto para ejecutar el git init.

Se puede realizar de dos maneras, yendo a la ruta y ejecutando `git init` ó ejecutando git init y pasando la ruta como parámetro `git <project directory>`

---

## Comandos

## Git clone

### Clonando un repositorio existente

Si el proyecto ya ha sido creado como un repositorio central, el comando de _git clone_, es la forma comúnmente más usada para obtener un clone de desarrollo local.
Al igual que git init, _git clone es una operación de un solo uso_, una vez que el desarrollador ha obtenido una copia funcional del proyecto, todas las operaciones de control de versiones, serán manejadas a través del repositorio local.

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
**_Son los medios para registrar versiones de un proyecto en el historial del repo._**

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

**_git no diferencia entre archivos supervisados en archivos y archivos nuevos que acaban de ser añadidos al repositorio._**

---

## Git commit

### Guardando cambios al repositorio

[Ver convención para los commits](https://www.conventionalcommits.org/es/v1.0.0-beta.2/#especificaci%c3%b3n)

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

**_Hay que tener en cuenta que por defecto git stash no incluye los archivos no trackeados o ignorados._**

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

Puedes ver un sumario de diferencias de un stash con _git stash show_:

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

---

## Git tag

En este apartado vamos a ver el concepto de etiquetar y los comandos de `git tag` las etiquetas son referencias a puntos en la historia de git. Son usados normalmente para apuntar a versiones de lanzamiento (v1.0). Una etiqueta es como una rama que no cambia, a diferencia de las ramas, las etiquetas después de ser creadas, no tienen más historial de commits en esa rama.
En este apartado cubriremos los difentes tipos de etiqueta, como crearlas, listarlas, borrarlas, compartirlas y más.

Creando etiquetas

Podemos crear una etiqueta con el siguiente comando.
git tag <tagname>

Reemplaza el tagname con un identificador semantico para el estado del repositorio. Un patron común es usar el número de version como git tag v1.4. Git soporta dos tipos de etiqueta, las etiquetas ligeras son esencialmente como marcapáginas para poner un nombre de puntero a un commit, muy útil para crear pequeños links a commits relevantes, una buena práctica es crear estas etiquetas como privadas.

---

Las etiquetas anotadas guardan información extra (Metadata). El nombre de quien crea la etiqueta, email y fecha, etc...

---

## Annotated Tags (etiquetas anotadas)

Las etiquetas anotadas son guardadas en la base de git como objetos completos. Para reiterar, guardan metadata como el nombre de quien etiqueta, el email o la fecha. Similar a los commits y los mensajes de los commits, las etiquetas anotadas tienen un mensaje de etiqueta. En adición por seguridad las etiquetas anotadas pueden ser firmadas con GNU privacy Guard (GPG). Las mejores prácticas suguieren que se usen annotated tags en lugar de etiquetas ligeras para tener más control ya que éstas guardan información adicional.

git tag -a v1.4

Ejecutando este comando crearemos una etiqueta aotada con el identificador v1.4. El comando abrirá una ventana adicional, para insertar información adicional.

git tag -a v1.4 -m "my version 1.4"

Este comando es similar a la ejecución anterior, pero con el parametro adicional de -m podemos crear el mesaje de la etiqueta como hacemos con el commit -m para no tener que insertarlo después desde el editor de texto.

---

## Etiquetas ligeras (lightweight tags)

git tag v1.4-lw

Ejecutando este comando podemos crear una etiqueta ligera identificada como v1.4-lw. Éstas etiquetas son creadas sin -a -s o -m.
Éstas etiquetas son creadas como un comprobante de etiqueta y almacenadas en .git/directorio del repositorio del proyecto.

---

## Listing tags (listar etiquetas)

Podemos mostrar una lista de las etiquetas guardadas con:

git tag

Para tener más control sobre la lista de etiquetas mostradas podemos pasar el parametro -l con una expresión definida:

git tag -l _-rc_

$ git tag -l _-rc_
v0.10.0-rc1
v0.11.0-rc1
v0.12.0-rc1
v0.13.0-rc1
v0.13.0-rc2
v0.14.0-rc1
v0.9.0-rc1
v15.0.0-rc.1
v15.0.0-rc.2
v15.4.0-rc.3

el prefijo -rc se usa por convencion para determinar release candidates\_

---

## Tagging old commits (Etiquetando viejos commits)

En el ejemplo anterior hemos usado la etiqueta para adjuntarla al commit que esté en la cabecera en ese momento como referencia. Pero podemos usar el tag en un commit especifico para etiquetar viejos commits. Podemos ver una lista de los commits con git log.

Podemos crear el tag para el commit especifico pasandole el id.

git tag -a v1.2 15027957951b64cf874c3557a0f3547bd83b3ff6

Ejecutando este comando de git crearemos una nueva etiqueta anotada con el identificador v1.2 para el commit que seleccionamos en el ejemplo anterior de git log.

---

## Reetiquetando o reemplazando etiquetas.

Al intentar crear una etiqueta con un identificador diferente donde ya existía una etiqueta anterior, git nos mostrará este error:

fatal: tag 'v0.4' already exists

En adición si intentamos etiquetar un commit anterior con un identificador de etiqueta ya existente, nos arrojará el mismo error.

Para este caso deberíamos actualizar la etiqueta existente y lo podemos hacer con la opción de -f (force).

git tag -a -f v1.4 15027957951b64cf874c3557a0f3547bd83b3ff6

**_Cuando forzamos un identificador ya usado, este se colocará en el nuevo commit y se borrará del commit anterior, esto sucede por que solo podemos tener un identificador único en la historia de git._**

## Sharing: Pushing Tags to Remote

Compartir etiquetas es similar a pushear ramas. Por defecto, git push no pasará las etiquetas. Éstas deben ser pasadas explicitamente al git push.

git push origin v1.4
Counting objects: 14, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (12/12), done.
Writing objects: 100% (14/14), 2.05 KiB | 0 bytes/s, done.
Total 14 (delta 3), reused 0 (delta 0)
To git@bitbucket.com:atlasbro/gittagdocs.git \* [new tag] v1.4 -> v1.4

Para pushear varias etiquetas simultaneamente, podemos pasar el parametro --tags cuando usemos el comando git push. Cuando otros usuarios clonen o puleen el repo, reciviran las nuevas etiquetas.

## Checking 0ut Tags.(comprobando etiquetas)

git checkout v1.4

El comando de arriba comprobará la etiqueta v1.4. Esto pondrá el repositorio en un header separado. Esto significa que cualquien cambio realizado en este header no será reflejado en la etiqueta.
Se creará un nuevo commit separado. Éste nuevo commit separado no será parte de ninguna rama y solo será accesible directamente por la persona que referencie dicho hash.
De todas formas las buenas prácticas recomiendan que crees una rama, si vas ha hacer cambios en un header separado.

## Deleting tags (borrando etiquetas)

Para borrar etiquetas lo hacemos directamente pasandole el parámetro -d y un identificador de etiqueta, ésto borrará el identificador de etiqueta.

git tag -d v1

---

## Git Blame

Git status/ git tag/ git blame

Git blame es un comando para resolución de problemas que a alto nivel, lo que hace es mostrar la metadata, perteneciente a líneas de código que han sido comiteadas en un archivo. Esto nos sirve para saber que, quién y por que x código ha sido añadido al repositorio.
También nos muestra el historial completo de edición de dicho código.

Git blame comunmente es usado con GUI display, un sitio de hosting para Git como bitbucket. El cual ofrece una vista con interfaz para git blame. Esas vistas sirven para discutir acerca de quien ha hecho un pull request o un commit. Adicionalmente, la mayoría de IDE´s que tienen integración con git, suelen tener también vistas del blame.

# How it works

Podemos usarlo de varias formas especificando algunos imputs, para que nos devuelva una salida más detallada, en base a lo que queramos sabes acerca de la edición de los archivos, a continuación mostramos los diferentes ejemplos:

git blame

Con este comando simple, lo que sacamos por consola es una lista del uso de dicho comando.

git blame Readme.md

Ejecutando este comando tendremos una primera vista de como funciona este comando. Este nos devoverá un subconjunto de la salida completa del archivo que mira. Adicionalmente esta lectura, es estatica al momento del repositorio que se está escribiendo.

comando con referencia de id de un commit
git blame Readme.md d2b8707c4fee5ce3a618a90502e1c780db8307c0

La salida de este blame nos mostrará valores tal que así:

id d2b8707c4fee5ce3a618a90502e1c780db8307c0
Author Paquito
Timestamp 2018-03-01 00:54:03 +0000
Line Number Muestra la línea que se ha modificado.
Line Content Muestra el contenido editado dentro del archivo.

# Common options

git blame -L 1,4 Git.md

La opcion de -L nos sirve para especificar una orquilla de líneas a comprobar, en este caso estaríamos comprobando de dicho archivo, las líneas de la 1 a la 4.

git blame -w Git.md

La opción de -w ignora los cambios de los espacios en blanco, por ejemplo si un autor anterior, ha cambiado de entre tabs y espacio, esto por desgracia ocuparía espacio innecesario en la salida del git blame.

git -M Git.md

Esta opción nos muestra que líneas han sido movida o copiadas, nos mostrará también el d autor original y no el que realizó estos cambios.

git blame -C

Esta opción nos muestra que líneas han sido copiadas o movidas de otros archivos. Nos muestra el autor original en lugar del autor que copió o movió dichas líneas.

## Git blame vs Git log

Mientras que git blame nos va a mostrar el autor que modifica o copia líneas en un archivo, para extraer el autor original puede ser complicado y tenemos que usar la combinación de -w -C -M. En estos casos será más fácil usar git log.

Para listar todos los commits originales, en los cuales piezas de código han sido añadidas o modificadas, usaremos el comando git log con la opcion -S.

Para comprobar en un archivo si una línea ha sido modificada, podemos pasarla como parametro al git log -S de ésta manera.

git log -S "línea a comprobar de un archivo".

---

## Deshaciendo commits y cambios

git checkout/ git clean/ git revert/ git reset/ git rm

En esta sección, hablaremos sobre las opciones disponibles para volver atrás o a una versión anterios con estrategias de comandos en git. Es importante aclarar que Git no tiene la típica opción de volver atrás como cualquier otro editor de texto.
En git no tenemos el típico comando "undo" git usa su propia nomenclatura para los comandos que nos dejarán volver atrás y la mentalidad de "undo" en git es diferente.
Algunas de los terminos que usamos en git son:
reset, revert, checkout, clean y más.

Una metafora graciosa es pensar en que git es una utilidad de manejo de la linea de tiempo.

Los commmits son isntantaneas, de un punto de interés a lo largo de la línea de tiempo. Adicionalmente, múltiple líneas de tiempo se dan lugar y pueden ser manejadas como ramas "branches". Cuando usamos comandos tipo "undo" lo que hacemos realmente es volver atrás en el tiempo o moverlos a otra rama temporal, donde los errores, no se han dado lugar.

Éste tutorial, te proveerá de las habilidades necesarioas para trabajar con revisiones anteriores de un proyecto. Primero, te muestra como explorar viejos commits y te explicará la diferencia entre revertir commmits públicos en el proyecto en contra de resetear cambios no publicados en tu proyecto local.

## Encontrando lo que se ha perdido

Revisando viejos commits

Toda la idea de tener un soft de control de versiones es poder guardar copias seguras de tu proyecto para no tener que preocuparte de fallos irreparables que rompan tu código por completo. Una vez que has construido un historial de commits en tu proyecto, puedes revisar y revisitar cualquier commit en la historia.
Una de las utilidades para revisar el historico de los commits sería el comando git log.

Cada commit tiene un id con un hash único. Éstos id´s son usados para viajar a lo largo de la línea de tiempo y revisitar los commits.
Por defecto, git log mostrará solo los commits referentes a nuestra rama de trabajo. Pero podemos ver los commits historicos de otras ramas con el comando:

git log --branches=\*

El comando git branch es usado para ber y visitar otra ramas.
El comando git branch -a nos devolverá una lista de todas las ramas conocidas con su nombre.
Uno de éstos nombres de rama puede ser luego usado para ver los logs especificos de esa rama:

git log --branches="main\*" no tiene el back slash

Cuando has encontrado la referencia del commit en un punto de la historia que queires visitar, puedes utilizar el comando gir checkout para visitar ese commit. git checkout es una forma fácil de cargar uno de estos puntos de guardado en tu maquina local.
Cuando hacemos un checkout, el header deja de apuntar a una rama, como master o main, y apunta directamente a un commit, con lo cual el header actual estará desconectado de cualquier rama.

# Visualizando una vieja revisión

En este ejemplo asumimos que has empezado a desarrollar como loco de una forma experimentar, pero no estás seguro de su quieres mantener los cambios o no. Para ayudarte a decidir puedes echar un vistazo al estado del proyecto antes de que empezaces a experimentar.
Primero deberías encontrar la referencia ID de la revisión que quieres ver.

## Deshaciendo un commit

Hay muchas estrategias que podemos tomar para deshacer un commit. En este ejemplo tendríamos un commit que se vería tal que así:

git log --oneline

Vamos a centrarnos en deshacer el 123412347 vamos a intentar algunas cosas medio locas ahora, así que esto se puede descontrolar un poco.

# Como deshacer un commit con git checkout

# Como deshacer un commit público con git revert

Vamos a asumir que volvemos a la historia original del ejemplo.
Ésta historia incluye el commit con referencia 82fa7e. Vamos a probar con git revert HEAD, si ejecutamos esto, git creará un nuevo commit con la inversión hasta el último commit. Ésto añadirá un nuevo commit hasta la historia de la rama actual y se vería tal que así:

git log --oneline

En este punto técnicamente hemos deshecho los cambios del commit 872fa7e. Y además todavía existe en la historia de git. El nuevo commit e2f9a78 ha invertido los cambios hasta 872fa7e, en diferencia a nuestra estrategia de reversión con git checkout, seguimos usando la mísma rama. Esta solución es una forma de deshacer satisfactoria, es el undo ideal para trabajar en repositorios públicos compartidos. Si te exigen mantener git de un modo más minimalista y limpio, ésta quizás no es la estrategia mas adecuada para ello.

## Como deshacer un commit con git reset

Deshaciendo el último commit

En la sección anterior, hemos visto varias formas de deshacer commits. Esas estrategias son aplicables a la mayoría de los commits recientes. En algunos casos quizás no necesitas borrar o resetear dichos commits, quizás solo te equivocaste al crear dicho commit o lo hiciste de forma prematura. En éste caso podemos usar amend en el commit más reciente. Una vez que has realizado cambios en tu proyecto de trabajo y los has supervisado con git add, puedes ejecutar el comando git commit --amend. Esto abrirá un editor de texto en para que puedas editar el mensaje del commit. Los cambios serán añadidos al commit en cuestión.

git commit --amend

## Deshaciendo cambios que no están comiteados

Antes de que los cambios sean comiteados a la historia del repo, se encuentran en el indice de estado y en el directorio del proyecto. Quizás necesitas deshacer los cambios a través de esas dos areas.
ambos son mecanismos del manejo de estado de git internamente.
Para saber más en profundidad como ambos mecanismos funcionan puedes mirar más en profundidad, git reset.

# El directorio de trabajo

El directorio de trabajo generalmente está sincronizado con los archivos locales de tu pc. Para deshacer cambios en el directorio de trabajo puedes editar los archivos como normalmente lo harías en un editor de texto.
Git tienes varias herramientas para ayudarte a manejar el directorio de trabajo. El comango git clean en una utilidad muy conveniente para deshacer cambios en el directorio de trabajo. Adicionalmente git reset puede ser invocada con --mixec o --hard para aplicar un reset al directorio de trabajo.

# El indice de estado

El comando git add es usado para añadir cambios al indice de estado. Git reset principalmente es usado para deshacer esos cambios.
Un --mixed reset moverá los cambios pendientes del indice de estado al directorio de trabajo.

# Deshaciendo cambios públicos

Cuando trabajamos en equipo con repositorios remotos, necesitamos una consideración extra para deshacer cambios.
Git reset debería ser considerado un método para deshacer a modo local.
Reset debe ser usado cuando deshacemos cambios a una rama privada.
Esto te prevendrá de borrar commits de otras ramas que quizás están en uso por otros desarrolladores. Los problemas comienzan, cuando un reset es ejecutado en una rama compartida y esta rama entonces es pusheada remotamente con git push.
Git blockeara el push en este escenario y se quejará de que la rama que está siendo pusheada está desactualizada de la rama remota o ha perdido algunos commits.

**_La mejor forma para deshacer cambios en una rama compartida será git revert_**

Un revert es mucho más seguro de usar en una rama compartida en lugar de un reset, por que no borrará commits de la historia.

Éste método es más seguro para colaboraciones en remoto, porque el desarrollador remoto puede hacer pull de la rama y recibir el nuevo revert commit el cual deshace los cambios del commit no deseado.

---

## Git clean

git checkout/ git clean/ git revert/ git reset/ git rm

# Opciones comunes de uso.

El siguiente contenido muestra varios usos para git clean, varios casos y las líneas que acompañan este comando.

-n

La opción de -n realizará una ejecución en seco del comando git clean esto te muestra que archivos están siendo removidos sin que sean removidos como tal. Como una simulación de git clean.
Es una buena práctica ejecutar siempre un git clean -n antes que un git clean.

git clean -n Would remove untracked_file

La salida nos dirá que archivos no supervisados serán borrados con el comando git clean. Los directorios no trackeados no aparecen en la salida de git clean. Por defecto git clean no opera recursivamente en directorios. Esto es otro mecanismo de seguridad para prevenir borrados permanentes por accidente.

-f or --force

La opcion de force inicia el borrado actual de los archivos sin revision en el directorio actual. Force no requiere del comando clean.
La opcion de requireForce biene establecida como falso por defecto.
No borrará archivos o carpetas que aparezcan en el .gitignore sin trackear.
Ahora nos permite ejecutar en vivo git clean en nuestro repositorio de ejemplo:

git clean -f Removing untracked_file

git clean -f -d include directories

La opción -d le dice a git clean que además quieres borrar cualquier directorio que no esté en seguimiento, por defecto ignorará los directorios. Podemos añadir la opción -d a nuestro ejemplo anterior.

git clean -dn Would remove untracked_dir/ git clean -df Removing untracked_dir/

La opcion -dn es una versión simulada que incluye directorios sin seguimiento.
La opción -df forzará el borrado de los directorios sin seguimiento con el comando git clean.

-x force removal of ignored files

El comando -x con git clean añadirá también los archivos que no estén siendo seguidos en el .gitignore, es una buena práctica comprobar que la ruta donde ejecutamos el git clean, no esté afectando a otros directorios como el build, etc...
También es una buena práctica como con el resto de opciones tirar el comando a modo de simulación antes de ejecutar el git clean -x para saber que archivos sin seguimientos serán borrados.

git clean -xf

Como vemos aquí también podemos combinar ambas opciones para hacer una opción combinada, en este caso -xf forzara a borrar todos los archivos del directorio actual que no estén en seguimiento y cualquier archivo que sea ignorado.

## Modo de limpieza interactiva o git clean interactivo

Además de los comandos en la consola que hemos demostrado hasta aquí, git clean tiene también un modo interactivo que nos deja iniciar pasandole la opcion de -i.

git clean -di Would remove the following items:

Hemos iniciado una sesión con la opción de -d para borrar directorios sin seguimiento. El modo interactivo nos mostrará una alerta en la línea de comandos para aplicar los archivos sin seguimiento.

---

## Git revert
