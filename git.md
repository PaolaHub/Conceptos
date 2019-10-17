# GIT and GItHub

### Version
* **git --version**

### Buscar ayuda
* **git help**

#### Más informacion sobre un comando en particular:
* **git help commit**

### Configuración en GIT
* **git config --global user.name "Paola"**

* **git config --global user.email "paola.tapia1@gmail.com"**

Git trabaja mucho con la confianza

#### Ver configuracion
* **git config --global -e**

Para salir :q (enter) => Sin salvar
Para salir y guradar :wq (enter) => Salvando

### Para iniciar git en nuestro repositorio
* **git init**

### Ver el estado el repositorio, añadir y hacer un commit

#### Ver cambios
* **git status**. Ver el estado del repositiorio. 
* **git status -s**. s de silence. Información más resumida.
* **git status -s -b**. s de silence. b de branch. Información más resumida.

#### Escenario: Añadir y excluir
1. Añadir todos los archivos.
* **git add .**:  Agrega todos los archivos.
* **git add -A**: Agrega todos los archivos.
* **git add --all**: Agrega todos los archivos.
* **git add "*.txt"**: Todos los archivos del proyecto con extension txt.
* **git add *.txt**: Todos los archivos en el directorio que nos enocntremos con extension txt.
* **git add <lista de archivos>**: Agrega todos los archivos que listemos.
* **git add pdfs/*.pdf**: Agrega todos los PDFs dentro de la carpeta PDFs.
* **git add pdfs**: Agrega todos los archivos dentro de la carpeta pdfs.

2. Añadir un archivo
* **git add README.md**

3. Excluir del stage todos los archivos que tengan extension xml.
* **git reset file.xml**. Con "reset" bajamos del escenario un archivo subido con el comando "add". 
* **git reset**. Baja del escenario todo lo que se encuentre.
* **git reset *.xml**. Baja todos los archivos xml del directorio.

#### Commit. Subir lo que hay en el escenario.
* **git commit -m "Primer Commit"**. Se va hacer un commit de lo que está en el escenario.

### Deshacer cambios
Reconstruye el proyecto a como estaba en el último commit.
* **git checkout -- .**

### Ver los LOGs
* **git log**: Ver todos los logs
* **git log --oneline**. Para verlo en una sola línea. Más resumido
* **git log --oneline**. Para verlo en una sola línea.
* **git log --oneline --decorate --all --graph**

HEAD => ÚLTIMO COMMIT EN EL BRACH ACTUAL

### Creando un alias
* **git config --global alias.lg "log --oneline --decorate --all --graph"**. Crea el alias "lg". Ahora podemos llamar comando git lg.
* **git config --global alias.s "status -s -b"**. Crea el alias "s". Comando: git s.

Ver alias:
* **git config --global -e**.









