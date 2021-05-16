# Documentacion GIT español

En este repositorio se registrará y explicará las distintas funciones de git durante el proceso de aprendizaje de múltiples proyectos.

# Configuraciones de entorno

Estas son algunas de las configraciones que necesitamos al momento de comenzar a utilizar el **sitema de control de versiones - GIT**

```git
git config --global user.email
git config --global user.name
git config --global color.ui true
```
Para configurar el editor con el cual haremos las modificaciones, se hace de la siguiente manera:
```git
git config --global core.editor "code --wait"
```
Para más información visitar el siguiente [link](https://git-scm.com/docs/git-config)

# Comandos GIT

## Iniciar el repositorio: Git init

```git
git init [<name-repository>]
```
Con este código iniciamos el repositorio, *si colocamos un nombre*, este será asignado, caso contrario, tomará el nombre del directorio.

**Nota:** Un aspecto a tomar en cuenta es que si está en parentesis cuadrados, significa que es opcional (no obligatorio), y el comando puede correr sin ese argumento.

## Borrar el repositorio

En el caso de que quisieramos borrar el repositorio que iniciamos, este lo podemos hacer borrando el archivo en sí de manera forzada; de la siguiente manera:

```cmd
rm -rf <file-name>
```

## Mirar el status

Si queremos consultar el estado de la **staging** area, podemos utilizar el siguiente comando:

```cmd
git status
```

## Añadir archivos a la **staging area**: git add
Con git add podemos poner los archivos en la staging area. La cual puede ser pensada como la sala preliminar a la "publicación"  oficial.

![staging area](https://git-scm.com/images/about/index1@2x.png)

Los comandos son los siguientes:
Colocar al staging area un archivo específico
```cmd
git add <file-name>
```
Colocar todos los archivos
```cmd
git add -A
```
para ver que archivos podemos agregar
```cmd
git add -n <file-name>
```
## Quitar de la stage área
Si colocamos algo en la stage área para ser cargado al repositorio (commit), pero nos arrepentimos, entonces hacemos lo siguiente:
```git
git rm --cached <file-name>
```
El anterior código los cologa en el *working directory* o unstaged el archivo

En el caso de que simplemente queramos eliminarlo, entonces:
```git
git rm -f <file-name>
```

## los commits
En el caso de que ya queramos subir la información al repositorio (no confundir con el directorio remoto que está en github), utilizaremos los git commit.

Cuando queremos hacer el commit y además añadir un mensaje que describa el cambio:
```git
git commit -m "<message-to-send>"
```
Adicionalmente, si queremos que, en lugar de un nuevo commit, concatenar el actual commit (el que queremos hacer en este momento) con el anterior:
```git
git commmit -m "<message>" --amend
```

## Ver registro de los commit
Si queremos ver la historia o registro de nuestro proyecto, a través de los commits, podemos utilizar los siguiente comandos.
Para mostrar la historia de manera detallada:
```git
git log
```
Si deseamos verlos de una manera más reducida, entonces utilizamos:
```git
git log --oneline
```
Además, si queremos ver las ramas que se han venido creando:
```git
git log --oneline --graph
```
y si solo queremos los n ultimos commits; por ejemplo, los ultimo cuatro commits.
```git
git log -4
```
## los tag's
Los tag son anotaciones que se hacen al proyecto y nos permite hacer una referencia sustancial. Por ejemplo, documentar una nueva version.
```git 
git tag <float-number>
```
Con anotación. Importante resaltar que se hace referencia al **commit** actual.
```git 
git tag -a <float> -m "<anotacion>"
```
**Listar todos los tags**
```git 
git tag -l
```
Etiquetar un commit, es importante resaltar que el commit al que se hace referencia en uno antiguo, no el actual commit
```git 
git tag -a <float> <sha-commit>
```
Borrar un tag
```git 
git tag -d <tag-number-to-delete>
```
Para renombrar un tag:
```git 
git tag -f -a <tag-version> -m '<message>' <sha-commit>
```
**Nota:** la referencia que se utiliza \<float> es solo eso, una referencia, porque tambien se pueden utilizar letras o cualquier patron que el desarrollador crea conveniente.

## Diferencias entre commits
Si queremos ver que ha cambiado entre dos commit, utilizamos:
```git
git diff <older-sha-commit> <more-recent-sha-commit>
```

## Volver en el tiempo
En el caso de que hayamos hecho mal, podemos regresar a los commits anteriores. Para dicho cometido, se hace uso de:
```git
git reset --[soft|mixed|hard] <sha-commit>
```
Aquí las diferencias principales son:
+ soft: deshace el último commit y coloca los archivos en la staging área
+ mixed: deshace el último commit y coloca los archivos en el working directory
+ hard: borra todo lo que se haya enviado con el commit anterior y en el staging area (no toca los untracked). Nota: se puede recuperar si conocemos el sha del último commit

## Configuraciones de las ramas (branch)
Para crear una nueva rama, utilizamos:
```git
git branch <new-branch-name>
```
Para enlistar todas las ramas del proyecto:
```git
git branch -l
```
Para borrar un rama:
```git
git branch -d <name-branch-to-delete>
```
En el caso de que no se borre facilmente, y tengamos que forzarlo:
```git
git branch -D <name-branch-to-delete>
```
Si necesitamos **renombrar** una rama:
```git
git branch -m <old-name> <new-name>
```
## Movernos entre ramas
si queremos cambiarnos de rama, utilizamos el siguiente código:
```git
git checkout <branch-name>
```
<font color='red'>
Nota: si utilizamos checkout y nos movemos a otra rama, sin guardar los cambios o utilizar <b>stash</b>, perderemos los cambios. El caso es mucho peor en las situaciones en donde <b>eliminamos archivos</b>; perderíamos los archivos y recuperarlos es un poco más complejo
</font>