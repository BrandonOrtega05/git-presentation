---
theme:
    override:
        code:
            theme_name: halcyon
---
<!-- column_layout: [1,2] -->
<!-- column: 0 -->

<!-- jump_to_middle -->
# **Git intermedio**

Mitsiu Alejandro Carreño Sarabia
<!-- column: 1 -->
![](./assets/memorizingsixgitcommands-big.png)

<!-- reset_layout -->


<!-- end_slide -->

# tree Temario
---
├── Intro   
│   ├── ¿Dónde esta el mouse?   
│   └── ¿Qué significa el comando?   
├── Config   
│   ├── Configurar su editor de textos    
│   ├── PS1    
│   ├── Configurar username / email       
│   └── Autenticación SSH   
├── Basics   
│   ├── Git workflow (Read your outputs)    
│   └── Git for dummies (Cheatsheet)    
├── Malabares locales   
│   ├── git branch   
│   ├── Stashing   
├── Malabares remotos   
│   ├── Cherry-picking   
│   └── git rebase vs git merge (Qué/Cómo/Cuándo)    
├── F&#42;ck ups   
│   ├── F&#42;ck up sencillo; mensaje de commit (--amend)   
│   ├── F&#42;ck up sencillo (git reset HEAD~1)   
│   ├── F&#42;ck up intermedio (subir a *-R) [modo fácil] (cherry-pick & delete branch)   
│   ├── F&#42;ck up intermedio (subir a *-R) [modo difícil](??)    
│   ├── F&#42;ck up complicado (rebase -i)   
│   ├── Mega f&#42;ck up (subir algo mal)   Agregar git revert y git revert -m 1 SHA1     
│   └── Who f&#42;ck up?   
└── Extras   
&nbsp;&nbsp;&nbsp;&nbsp;├── git add -p   
&nbsp;&nbsp;&nbsp;&nbsp;├── Origins   
&nbsp;&nbsp;&nbsp;&nbsp;└── Submodules   

<!-- end_slide -->
### Intro
#### Convenciones
---

Bloques de código, con highlight:
```bash {all|1|2-4|all}
$ git log --oneline
3cf53b0 (HEAD -> UNA-10) feat: UNA-10 1 commit
70196b3 (main) Add filder struct and add titles
84e3445 (origin/main) Upload wip presentation
```
Donde: 
- $ = comando

<!-- pause -->

Hasta abajo de mi pantalla hay dos cuadros ```"Slides"``` y ```"Terminal"``` el activo se marca en color verde

<!-- column_layout: [1,1] -->
<!-- column: 0 -->
Bloques de código ejecutables:
```bash +exec
# 🤖 : Este emoji es porque voy a ejecutar el 
# código dentro de la presentación
echo "Hola mundo"
```
<!-- column: 1 -->
```bash
# 🐱‍💻: Este otro emoji es porque voy a ejecutar
# código en la pestaña "Terminal"
ps aux
```

<!-- reset_layout -->

<!-- end_slide -->
### Intro
#### ¿Dónde esta el mouse?
---

En mi experiencia teclear es `más rápido` que usar el mouse.
* Misclicks
* Perder el puntero
* Arrastrar hasta el botón

![](./assets/mouse_pointer.gif)
    
Así que uso el teclado!
    
Pero ustedes usen lo que les hace sentir más comodos, pueden `aprender a usar el teclado` o pueden explorar y `aprender y configurar su interfaz gráfica` de preferencia. 

<!-- end_slide -->
### Intro
#### ¿Qué significa el comando?
---

La formula general para cualquier comando de git es    
`git <command> <args>`      
cuando tengan dudas usen     
`git <command> --help` o usen [](https://git-scm.com/docs)

¿Cómo sé la formula general?
```bash
$ git --help
usage: git [-v | --version] [-h | --help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           [--config-env=<name>=<envvar>] <command> [<args>]
```

Donde:
- [] = Un argumento/comando opcional 
- | = otra manera de llamar el mismo argumento/comando
- <> = algo variable

<!-- end_slide -->
### Intro
#### ¿Qué significa el comando?
---
```bash
$ git --help
usage: git [-v | --version] [-h | --help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           [--config-env=<name>=<envvar>] <command> [<args>]
```

```bash +exec
🤖
# Ejecutando
git -v
# Es igual a 
git --version
```

🐱‍💻 Veamos el resultado completo de `git --help`

<!-- end_slide -->

### Config
#### Configurar su editor de textos 
---
Primero es importante `configurar un editor de textos` con el que se sientan cómodos, puede ser de interfáz gráfica o de terminal.

Para configurar el editor pueden usar el siguiente comando remplazando &lt;path&gt;:
   
**Nota: Esta opción cambia la configuración global (afecta a todos los repos)**
```bash
🐱‍💻
git config --global core.editor "<path>"
# Ejemplos:
git config --global core.editor "vim"
git config --global core.editor "nano"
git config --global core.editor "gnome-text-editor"
```

<!-- end_slide -->

### Config
#### Configurar Visual Studio Code
---

```bash
code --help
```

> if you do not see help, please follow these steps:
> - Mac: Type Shell Command: Install 'Code' command in path from the Command Palette.
> Command Palette is what pops up when you press shift + ⌘ + P while inside VS Code. (shift + ctrl + P in Windows)
> - Windows: Make sure you selected Add to PATH during the installation.
> - Linux: Make sure you installed Code via our new .deb or .rpm packages.
> 
> https://stackoverflow.com/a/36644561

```bash
# Visual studio code
git config --global core.editor "code --wait"
# O ruta completa
git config --global core.editor "<path/to/code> --wait"
```

<!-- end_slide -->

### Config
#### Configurar su editor de textos 
---
Verifiquemos nuestra configuración corriendo:

```bash
🐱‍💻
git config --global -e
```

<!-- end_slide -->

### Config
#### Configurar su editor de textos 
---
Extra: Podemos listar los archivos de configuración con:
```bash +exec
🤖
git config --list --show-origin
```

<!-- end_slide -->

### Config
#### PS1 
---
<!-- column_layout: [6, 1] -->
<!-- column: 0 -->
> The PS1 Shell Variable
> The PS1 shell variable defines the text printed before the blinking cursor in our terminal. 
> We may set a simple value like a single character, for example, $ or #. 
> On the other hand, we may set complex expressions 
> that are evaluated when the prompt is printed.
> 
> https://www.baeldung.com/linux/customize-bash-prompt
<!-- column: 1 -->
![](./assets/ps1.png)
<!-- reset_layout -->

🐱‍💻

https://gist.github.com/mitsiu-carreno/b2ed36387ff4157f44002dda8bf81798#file-git-prompt-sh

> Credito: Shawn O. Pearce 

Linux

```bash
# Fedora (/etc/bashrc)
source ~/.git-prompt.sh
[ "$PS1" = "\\s-\\v\\\$ " ] && PS1="\u@\W\[\033[32m\]\$(__git_ps1)\[\033[00m\] $ "
```

<!-- end_slide -->

### Config
#### PS1 
---
Mac

```bash
source ~/.git-prompt.sh
# Mac (~/.bashrc)
export PS1="\u@\W\[\033[32m\]\$(__git_ps1)\[\033[00m\] $ "
```

Widows (WSL)

```bash
source ~/.git-prompt.sh
# WSL Linux (~/.bashrc)
PS1='${VIRTUAL_ENV:+($(basename $VIRTUAL_ENV)) }${debian_chroot:+($debian_chroot)}
\[\033[00m\]\u@\W\[\033[32m\]$(__git_ps1 " (%s)")\[\033[00m\] $ ';;
```


<!-- end_slide-->


### Config
#### user.name & user.email
---
Usualmente queremos tener nuestra `cuenta personal` separada de nuestra `cuenta de trabajo`
![](./assets/mike.png)

<!-- end_slide -->

### Config
#### user.name & user.email
---

Personalmente divido mis cosas del trabajo en una subcarpeta `*/designa/`

```bash
$ tree -L 2 Documents/
Documents/
├── designa
│   ├── acuerdo-286
│   ├── administracion-usuarios-causanatura
│   ├── aprendizajes-para-todos
│   ├── avicola.app
│   ├── causa-natura-media
│   ├── database_backup
│   ├── devops
│   ├── privasol.mx
│   ├── servicios-escolares
│   └── ssh
├── dev_hell
│   ├── crunch-test
│   ├── cmake_tutorial
│   └── git-presentation
└── upa
    ├── oop
    └── plat_web
```


<!-- end_slide -->

### Config
#### user.name & user.email
---
<!-- column_layout: [2, 1] -->
<!-- column: 1 -->
![](./assets/lobos.png)
<!-- column: 0 -->

Personalmente divido mis cosas del trabajo en una subcarpeta `*/designa/`

~/.gitconfig
```bash {all|1-3|4-5|all} +line_numbers
[user]
  name = mitsiu-carreno
  email = mitsiu.carreno@gmail.com
[includeIf "gitdir:*/designa/"]
  path = .gitconfig.designa
[includeIf "gitdir:*/upa/"]
  path = .gitconfig.upa
[core]
  editor = vim
```
<!-- pause -->

~/.gitconfig.designa
```bash +line_numbers
[user]
  name = designa-mitsiu
  email = mitsiu.carreno@designamx.com
```

<!-- end_slide -->

### Config
#### Autenticación SSH
---

Finalmente es posible tener multiples llaves ssh y asignar cada una a una cuenta de github, en este caso basado en una subcarpeta `*/upa/` se referencía a la llave id_ed25519_upa

~/.ssh/config
```bash {all|1-2|4-5|all} +line_numbers
Match host github.com exec "[ $(pwd | egrep -ic 'designa') = 1 ]"
  IdentityFile ~/.ssh/id_ed25519_designa

Match host github.com exec "[ $(pwd | egrep -ic 'upa') = 1 ]"
  IdentityFile ~/.ssh/id_ed25519_upa

Host github.com
  IdentityFile ~/.ssh/id_ed25519
```

Para más información [](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

<!--end_slide -->

### Basics
#### Git workflow (Read your outputs)
---

![](./assets/git-workflow.png)

- **Working directory** => El área donde podemos `ver, crear, borrar, editar etc.` Git no da seguimiento de estos archivos `untracked files`

```bash {all|1|3-9|5|6|all}
$ touch new_file #Crear archivo nuevo

$ git status
On branch feature-1
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	new_file

nothing added to commit but untracked files present (use "git add" to track)
```

<!--end_slide -->


### Basics
#### Git workflow (Read your outputs)
---

![](./assets/git-workflow.png)

- **Working directory** => El área donde podemos `ver, crear, borrar, editar etc.` Git no da seguimiento de estos archivos `untracked files`

```bash {all|1|3-10|5|6-7,10|all}
$ echo "Modificar archivo commiteado" > modif_file # Agregar texto a archivo existente

$ git status
On branch feature-1
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   modif_file

no changes added to commit (use "git add" and/or "git commit -a")
```

<!--end_slide -->

### Basics
#### Git workflow (Read your outputs)
---

![](./assets/git-workflow.png)

- **Index/Staging** => El área en que git comienza a dar `seguimiento de los archivos y a guardar sus cambios`

```bash {all|1|4-8|5,7-8|6|all}
$ git add modif_file new_file

$ git status
On branch feature-1
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   modif_file
	new file:   new_file
```

<!--end_slide -->

### Basics
#### Git workflow (Read your outputs)
---

![](./assets/git-workflow.png)

- **HEAD** => Un `apuntador al commit más reciente de la rama actual`

<!-- pause -->

Pero... `¿Qué es un commit?`

<!--end_slide -->

### Basics
#### Git workflow (Read your outputs)
---

<!-- column_layout: [2,1] -->
<!-- column: 0 -->
- **HEAD** => Un `apuntador al commit más reciente de la rama actual`
- **Commit** => Comando para `capturar el estado` (index/stage) de punto en el tiempo

Imáginemos git como el juego adivina quién, con unas modificaciones...
<!-- column: 1 -->
![](./assets/adivina-quien-guess-who.gif)
<!-- reset_layout -->

<!-- pause -->
*En nuestra versión del juego primero movemos las fichas y luego preguntamos
- Cada pregunta es un mensaje de commit 
```bash
git commit -m'¿Tu personaje tiene barba?'
```
- Cada commit tiene asociado un cambio de estado 
```bash
git add bill
git rm sofie
```

<!--end_slide -->

### Basics
#### Git workflow (Read your outputs)
---

- **HEAD** => Un `apuntador al commit más reciente de la rama actual`
- **Commit** => Comando para `capturar el estado` (index/stage) de punto en el tiempo

![](./assets/head.gif)
> Credito: https://www.youtube.com/@themoderncoder
<!--end_slide -->

### Basics
#### Git workflow (Read your outputs)
---

- **HEAD** => Un `apuntador al commit más reciente de la rama actual`
- **Commit** => Comando para `capturar el estado` (index/stage) de punto en el tiempo

<!-- column_layout: [1,1] -->
<!-- column: 0 -->

**Agregar y commitear**  
```bash 





$ git add new_file
$ git commit -m'adding new file'
[feature-1 70f6e27] adding new file
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 new_file



$ git add modif_file
$ git commit -m'modif exist file'
[feature-1 dd574be] modif exist file
 1 file changed, 1 insertion(+)
```
<!-- column: 1 -->
**Historial de commits**
```bash 
$ git log --graph --oneline
* ecf4186 (HEAD -> feature-1) Setting up 



$ git log --graph --oneline
* 70f6e27 (HEAD -> feature-1) adding new file
* ecf4186 (origin/feature-1) seting up prev commit





$ git log --graph --oneline
* dd574be (HEAD -> feature-1) modif exist file
* 70f6e27 adding new file
* ecf4186 (origin/feature-1) seting up prev commit
```

<!-- reset_layout -->

<!--end_slide -->

### Basics
#### Git workflow (Read your outputs)
---

![](./assets/git-workflow.png)

- **Remote repo** 

```bash {all|1|9|all}
$ git push origin feature-1
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 12 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (5/5), 520 bytes | 520.00 KiB/s, done.
Total 5 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To github.com:mitsiu-carreno/git-interm-presentation.git
   ecf4186..dd574be  feature-1 -> feature-1
```

<!--end_slide -->

### Basics
#### Git para dummies
---

![](./assets/commands.png)

<!--end_slide -->

### Basics
#### Git para dummies (Cheatsheet)
---


```bash +line_numbers
# Crear repo local
git init

# Clonar repo remoto
git clone <URL>

# Obtener el estatus actual del repositorio
git status

# Seguimiento de los cambios de un archivo 
git add <file1> <file2>

# Crear un nuevo commit y agregar un mensaje
git commit -m'<Descrip de cambios>'

# Obtener los cambios del repo remoto
git pull origin <branch>

# Subir cambios al repo remoto 
git push origin <branch>
```

*origin => remote name

<!--end_slide -->

### Malabares locales
#### git branch (Cheatsheet)
---


```bash +line_numbers
# Crear una nueva rama, y cambiar el workspace
git checkout -b <new-branch>

# Mostrar todas las ramas locales y remotas
git branch --all

# Cambiar el directorio de trabajo a otra rama
git checkout <branch>

# Borrar rama local integrada a main 
# (con directorio de trabajo en otra rama)
git branch -d <rama>

# Borrar rama local no integrada a main
# (con directorio de trabajo en otra rama)
git branch -D <rama>

# Unir dos ramas (genera nuevo commit)
git merge <branch>

# Borrar rama remota 
git push origin --delete <branch>
```

*origin => remote name

<!-- end_slide -->

### Malabares locales
#### Stashing
---

Permite guardar los cambios del directorio de trabajo e index pero a la vez, permitiendo regresar a un directorio de trabajo limpio.

Casos de uso:
- Cambios necesarios en local que `nunca deben subirse al repo` remoto (.env, config individuales, código de depuración)
- Cambios locales momentaneamente irrelevantes para un fix urgente (queremos mantener los cambios solo de manera local, pero `queremos un directorio de trabajo limpio para resolver un bug`)

```bash {all|3-5|6-9|10-12|all}
$ git status
On branch UNA-25
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
    new file:   test
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
    modified:   nginx.conf
Untracked files:
  (use "git add <file>..." to include in what will be committed)
    queries
```
<!-- end_slide -->

### Malabares locales
#### Stashing
---

Guardando en stash

```bash {1-5|7-13|15-19|all} 
$ # git stash
$ # git stash push 
$ # git stash push -- nginx.conf test
$ git stash -m"My new stash" -- test nginx.conf
Saved working directory and index state On UNA-25: My new stash

$ git status
On branch UNA-25
Untracked files:
  (use "git add <file>..." to include in what will be committed)
    queries

nothing added to commit but untracked files present (use "git add" to track) 

$ git stash list
stash@{0}: On UNA-25: My new stash
stash@{1}: WIP on UNA-18: 7ff5ee3 fix: UNA-18 Allow single questions be omitted
```
**Nota: El stash más reciente siempre tiene el indice 0**

<!-- end_slide -->

### Malabares locales
#### Stashing
---

Recuperando de stash

```bash {1-4|6-21|21|all} +line_numbers
$ git stash show 0
 nginx.conf | 1 +
 test       | 0
 2 files changed, 1 insertion(+)

$ git stash pop 0
On branch UNA-25
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   test

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   nginx.conf

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	queries

Dropped refs/stash@{0} (a41ae5cabf5c0de873e2bd2b872984538e3c46aa)
```

<!-- end_slide -->

### Malabares locales
#### Stashing
---

> git stash --help [pop]
> Applying the state can fail with conflicts; in this case, it is not removed from the stash list. 
> You need to resolve the conflicts by hand and call git stash drop manually afterwards.

***Cuando tengan duda si recuperaron su stash correctamente**
```bash +line_numbers
git stash list
```

<!-- end_slide -->

### Malabares remotos
#### Cherry-picking
---

Permite aplicar commits existentes en el directorio de trabajo actual.

Casos de uso:
- Hicieron y publicaron `(pushearon) commits en una rama equivocada.`
- Necesitan de manera urgente `cierto commit de otra rama (pero no toda la rama)` [ej, dependencia de una rama en progreso] 

**Importante: Por simplicidad, cuando decidan usar cherry-pick asegurense de que una de las dos siguientes condiciones se cumpla:**
- `La rama de donde copiaron los commits se va a borrar`
- `Los archivos relacionados al commit que copiaron no se van a modificar hasta que se merge con main o la rama de donde se copió`

<!-- end_slide -->

### Malabares remotos
#### Cherry-picking
---

Ejemplo: Se creo la rama incorrecta UNA-10 en lugar de UNA-11 **Nota:** Nadie esta trabajando el issue UNA-10 por lo que se puede borrar, pero queremos rescatar el trabajo avanzado
<!-- column_layout: [1, 1] -->
<!-- column: 0 -->
Setup
```bash 
$ git log --oneline
531d90d (HEAD -> UNA-10) commit 4
2f0b408 commit 3
c8df2a7 commit 2
28eacf7 commit 1
70196b3 (main) Add filder struct and add titles
```

<!-- column: 1 -->

![](./assets/cherry-p_1.png)
 
<!-- end_slide -->

### Malabares remotos
#### Cherry-picking
---

Ejemplo: Se creo la rama incorrecta UNA-10 en lugar de UNA-11 **Nota:** Nadie esta trabajando el issue UNA-10 por lo que se puede borrar, pero queremos rescatar el trabajo avanzado
<!-- column_layout: [1, 1] -->
<!-- column: 0 -->
Setup
```bash 
# Regresamos a la rama principal (¿Por qué?)
$ git checkout main
# Actualizamos nuestra rama local (¿Por qué?)
$ git pull origin main
```

<!-- column: 1 -->
<!-- pause -->
![](./assets/cherry-p_2.png)
 
<!-- end_slide -->

### Malabares remotos
#### Cherry-picking
---

Ejemplo: Se creo la rama incorrecta UNA-10 en lugar de UNA-11 **Nota:** Nadie esta trabajando el issue UNA-10 por lo que se puede borrar, pero queremos rescatar el trabajo avanzado
<!-- column_layout: [3, 1] -->
<!-- column: 0 -->
Setup
```bash
# Creamos la rama correcta
$ git checkout -b UNA-11
Switched to a new branch 'UNA-11'
$ git log --oneline
70196b3 (HEAD -> UNA-11, main) Add filder struct and add titles
```

<!-- column: 1 -->

![](./assets/cherry-p_3.png)
 
<!-- end_slide -->

### Malabares remotos
#### Cherry-picking
---

Ejemplo: Se creo la rama incorrecta UNA-10 en lugar de UNA-11 **Nota:** Nadie esta trabajando el issue UNA-10 por lo que se puede borrar, pero queremos rescatar el trabajo avanzado
<!-- column_layout: [2, 1] -->
<!-- column: 0 -->
Setup
```bash
# Elegimos los commits a copiar a la nueva rama
$ git cherry-pick 28eacf7
[UNA-11 6f6b8d7] commit 1
 Date: Sat Mar 30 15:43:48 2024 -0600
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 git-interm/a

$ git log --oneline
6f6b8d7 (HEAD -> UNA-11) commit 1
70196b3 (main) Add filder struct and add titles
```
**Importante:** Noten que `generamos un nuevo commit`

<!-- column: 1 -->

![](./assets/cherry-p_4.png)
 
<!-- end_slide -->

### Malabares remotos
#### Cherry-picking
---

Ejemplo: Se creo la rama incorrecta UNA-10 en lugar de UNA-11 **Nota:** Nadie esta trabajando el issue UNA-10 por lo que se puede borrar, pero queremos rescatar el trabajo avanzado
<!-- column_layout: [2, 1] -->
<!-- column: 0 -->
Setup
```bash
# Elegimos los commits a copiar a la nueva rama
$ git cherry-pick c8df2a7
[UNA-11 0292526] commit 2
 Date: Sat Mar 30 15:44:04 2024 -0600
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 git-interm/b

$ git cherry-pick 2f0b408
[UNA-11 e440696] commit 3
 Date: Sat Mar 30 15:44:13 2024 -0600
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 git-interm/c

$ git cherry-pick 531d90d
[UNA-11 5b033f9] commit 4
 Date: Sat Mar 30 15:44:22 2024 -0600
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 git-interm/d
```
**Importante:** Noten que `generamos un nuevo commit`

<!-- column: 1 -->

![](./assets/cherry-p_5.png)
 
<!-- end_slide -->

### Malabares remotos
#### Cherry-picking
---

Permite aplicar commits existentes en el directorio de trabajo actual.

**Importante: Dado que se crean nuevos commits identicos a commits anteriores se debe tener cuidado de no generar conflictos:**
- `La rama de donde copiaron los commits se va a borrar`
- `Los archivos relacionados al commit que copiaron no se van a modificar hasta que se merge con main o la rama de donde se copió`
```bash
# Borrrar rama local
$ git checkout -D UNA-10
Deleted branch UNA-10 (was 531d90d)

# Borrar rama remota
$ git push origin --delete UNA-10
```

<!-- end_slide -->

### Malabares remotos
#### git rebase vs git merge (Qué/Cómo/Cuándo)
---

git-merge - Join two or more development histories together     
git-rebase - Reapply commits on top of another base tip     

Ambos comandos nos permiten integrar cambios entre dos ramas pero lo hacen de manera diferente.

Comencemos por merge que estamos familiarizados:

```bash
git init
touch a
git add a
git commit -m'main 1'
[master (root-commit) fe2058d] main 1
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 a

touch b
$ git add b
$ git commit -m'main 2'
[master 5bccf6f] main 2
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 b

git checkout -b merge-b
Switched to a new branch 'merge-b'
touch m-c
git add m-c
git commit -m'merge 1'
[merge-b a49858a] merge 1
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 m-c
$ touch m-d
$ git add m-d 
$ git commit -m'merge 2'
[merge-b 09f28ff] merge 2
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 m-d

git log --oneline
09f28ff (HEAD -> merge-b) merge 2
a49858a merge 1
5bccf6f (master) main 2
fe2058d main 1

#Adelantemos main (simulando que otro colaborador hizo merge)
touch c 
$ git add c
$ git commit -m'main 3'
[master 1340a20] main 3
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 c
$ git log --oneline
1340a20 (HEAD -> master) main 3
5bccf6f main 2
fe2058d main 1
$ git pull origin master

$ git checkout merge-b
Switched to branch 'merge-b'

```
```bash
Merge branch 'master' into merge-b
# Please enter a commit message to explain why this merge is necessary,
# especially if it merges an updated upstream into a topic branch.
#
# Lines starting with '#' will be ignored, and an empty message aborts
# the commit.

git merge master
Merge made by the 'ort' strategy.
 c | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 c

$ git log --oneline
0b8851e (HEAD -> merge-b) Merge branch 'master' into merge-b
1340a20 (master) main 3
09f28ff merge 2
a49858a merge 1
5bccf6f main 2
fe2058d main 1
```

<!-- end_slide -->

<!-- jump_to_middle -->
### F&#42;ck ups
Los f&#42;ck ups sencillos son aquellos que son locales, una vez que se suben al repo remoto se debe `tener sensibilidad sobre el riesgo de que alguien haya descargado los cambios a su repositorio remoto.`

Parecido al comando cherry-pick, estos comandos `literalmente estan cambiando la historia (commits nuevos que sustituyen a commits viejos).`

<!-- end_slide -->

### F&#42;ck ups
#### F&#42;ck up sencillo; mensaje de commit (--amend)
---
Dada la integración de semantic release [](https://github.com/semantic-release/commit-analyzer?tab=readme-ov-file#default-rules-matching) que usamos en los proyectos, los mensajes de commit deben tener un formato especifico para generar una nueva versión a deployar.

<!-- column_layout: [2,1] -->
<!-- column: 0 -->
```bash {all|1-7|9-18|all}
$ git commit -m'arreglar archivo'
[main (root-commit) 397c847] arreglar archivo
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 a

$ git log --oneline
397c847 (HEAD -> main) arreglar archivo

$ git commit --amend -m "fix: UNA-10 arreglar archivo"
[main f35029d] fix: UNA-10 arreglar archivo
 Date: Sun Mar 31 21:25:32 2024 -0600
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 a

$ git log --oneline
f35029d (HEAD -> main) fix: UNA-10 arreglar archivo

$ git push origin UNA-10
```
<!-- column: 1 -->

Aspectos a considerar:
- Estamos generando nuevos commits (`sustituyendo historia`) por lo que si el commit ya fue pusheado esta solución solo se debe emplear si estamos seguros que nadie ha descargado el primer commit (397c847).
- Amend `solo funciona para el último commit` (el más reciente)

<!-- reset_layout -->

<!-- end_slide -->

### F&#42;ck ups
#### F&#42;ck up; Deshacer último commit (reset)
---

Hay situaciones en las que acabamos de hacer un commit solo para darnos cuenta que faltó hacer algun otro cambio, o falto agregar otro archivo.

Es posible deshacer los últimos n commits:
- Regresando los archivos a index
- Descartando los cambios por completo


```bash
$ git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	a
	b
	c
	d
	e

nothing added to commit but untracked files present (use "git add" to track)
```

<!-- end_slide -->

### F&#42;ck ups
#### F&#42;ck up; Deshacer último commit (reset)
---
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
```bash
git add a && git commit -m'1 +a'
[main (root-commit) ab641d8] 1 +a
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 a
$ git add b && git commit -m'2 +b'
[main e940ab8] 2 +b
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 b
$ git add c && git commit -m'3 +c'
[main 757a605] 3 +c
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 c
$ git add d && git commit -m'4 +d'
[main 7087d5d] 4 +d
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 d
$ git add e && git commit -m'5 +e'
[main 21ae9ea] 5 +e
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 e
```

<!-- column: 1 -->

```bash
$ git log --oneline
21ae9ea (HEAD -> main) 5 +e
7087d5d 4 +d
757a605 3 +c
e940ab8 2 +b
ab641d8 1 +a

# Deshacer ultimo commit, mantener index y work dir
$ git reset HEAD~

$ git status
On branch main
Untracked files:
  (use "git add <file>..." [...]) 
	e

nothing added to commit but untracked files present 
$ git log --oneline
7087d5d (HEAD -> main) 4 +d
757a605 3 +c
e940ab8 2 +b
ab641d8 1 +a
```
<!-- reset_layout -->

<!-- end_slide -->

### F&#42;ck ups
#### F&#42;ck up; Deshacer último commit (reset)
---
<!-- column_layout: [1,1] -->
<!-- column: 0 -->
La opción `--hard` nos permite descartar completamente un commit
```bash
# Descartar completamente el último commit
$ git reset HEAD~ --hard
HEAD is now at 757a605 3 +c
$ git status
On branch main
Untracked files:
  (use "git add <file>..." [...])
	e

nothing added to commit but untracked files present
$ git log --oneline
757a605 (HEAD -> main) 3 +c
e940ab8 2 +b
ab641d8 1 +a
```
Se descartó completamente el archivo "d"

<!-- column: 1 -->

Para descartar mutliples commits basta con especificar cuantos commits detrás de HEAD

```bash
$ git reset HEAD~2
$ git status
On branch main
Untracked files:
  (use "git add <file>..." [...])
	b
	c
	e

nothing added to commit but untracked files present
$ git log --oneline
ab641d8 (HEAD -> main) 1 +a
```
<!-- reset_layout -->

<!-- end_slide -->

### F&#42;ck ups
#### F&#42;ck up; Deshacer último commit (reset)
---


<!-- end_slide -->

### F&#42;ck ups
#### F&#42;ck up; Deshacer último commit (reset)
---

$ git rebase HEAD~3
reword

<!-- end_slide -->

### F&#42;ck ups
#### 
---
<!-- end_slide -->

### F&#42;ck ups
#### 
---
<!-- end_slide -->

### Extras
#### add -p
---
<!-- end_slide -->

### Extras
#### Origins
---
<!-- end_slide -->

### Extras
#### Submodules
---
