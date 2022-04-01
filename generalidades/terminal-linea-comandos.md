# Terminal y línea de comandos
## Terminal
Es una interfaz gráfica que simula una línea de comandos.
Cuando se habla de línea de comandos hace referencia a una shell
## Línea de comandos(Shell)
Es un programa que toma comandos y los pasa al sistema operativo para hacer algo  
### Tipos de shell
- Bourne shell
- Bash shell
- Z shell
- C shell
- Korn shell
- Fish shell
- PowerShell
# Comando
Un comando puede ser:
* Un programa ejecutable
* Un comando de utilidad de la shell
* Una función de shell
* Un alias
## Comandos 
- ls: muestra el contenido de la carpeta ejm: ls -lh
- cd: Cambiar de directorio, recibiendo como parametro el nombre de la carpeta a la que se quiere acceder ejemplo: cd picture
- clear: Limpia la pantalla
- pwd: Muestra la ruta en la que se encuentra
- file: Describe un tipo de archivo
- tree: Muestara todas las carpetas, tree -L 1
- mkdir: Crea un directorio, mkdir miDirectorio
- touch: Crea un archivo
- cp: Copiar un archivo
- mv: Mover un archivo, mv miArchivo.txt ./
- rm: Elimnar un archivo, para eliminar una carpeta se usa rm -r
- head: Muestra la primeras 10 lineas del archivio, head -n 20
- tail: Muesta las ultimas 10 lineas del archivo, tail -n 20
- less: Muestra todo el archivo de texto
- xdg-open: Abre un archivo con el editor de texto predeterminado
- nautilus: Abre la carpeta que se le indique
- type: Permite ver la categoria del comando
- alias: Crear un alias, alias l="ls -lh"
- help: Información sobre el comando, help cd
- man: Manual de un comando, man cd
- info: Información de un comando, info cd
- whatis: Información corta de un comando, whatis cd
# Wildcards
Caracteres que ayudan en las busquedas y filtrado de buscqueda
- ls *.txt: busca todos los archivos que contenga al final .txt, ls datos* muestra todos los archivos que empiezan con datos
- ls datos?: Busca todas las palabras que tengan datos al inicio y solo un caracter al final, para 3 caracteres seria ls datos???
- ls [[:upper:]]*: Busca todos los contenidos que empiecen con mayusculas
- ls [ad]*: Busca todos los archivos que empiezan con ab
# Redirecciones
## File Descriptor
- 0: Standard input, salida de información para el input
- 1: Standard output, salida de información para el output
- 2: Standard error, salida de información para los errores

## > 
Guarda el output de la operación en un un archivo, creándolo o si existe lo sobrescribe
```sh
ls carpeta > listadoArchivos.txt
```
## >> 
Guarda el output de la operación en un un archivo, concatena el contenido en el archivo
```sh
ls carpeta2 >> listadoArchivos.txt
```
## 2>
Guarda en un archivo el error que arroje la operación
```
ls alskdjf 2> error.txt
```
## >> 2>&1
Redireccionar un error y un output
```
ls alsdkfj >> output.txt 2>&1
```
