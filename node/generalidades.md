# package.json
- name: Nombre del proyecto
- author: Autor del proyectos
- description: Descripción que resume el proyectos
- keywords: Palabras claves que describen el proyecto
- license: Tipo de licencia del proyectos
- version: Describe la versión actual del proyecto (Required)
- dependencies: Agregan las depencias que node instalara para el proyecto
- ~: Sirve para permitir que npm actualice los ultimos PATCH de una versión
- ^: Similar a ~ sirve para pemitir los ultimos PATCHes y MINOR 
```json
{
    "name": "fcc-learn-npm-package-json",
	"author": "Robinson Rosales",
	"description": "A project for learn manage Node.js",
    "keywords": [
		"freecodecamp",
		"learn",
		"node.js"
	],
    "license":"MIT",
    "version": "1.2.0",
    "dependencies": {
        "package-name": "version",
        "express": "^4.14.0",
        "moment": "~2.14.0"
    }
}
```
# semantica de versionamiento
```json
"package: "MAJOR.MINOR.PATHC"
```
- MAJOR: Incrementa cuando se hagan cambios de API incompatibles, son cambios que no son compatibles con versiones anteriores
- MiNOR: Incrementa cuando se agregan funcionalidades que sean compatibles con versiones anterioes, son nuevas features pero no rompen nada de lo anterior
- PATCH: Incrementa cuando se arregland bugs de versiones anteriores, son correciones de errores


