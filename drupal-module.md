# Módulos en Drupal
Son elementos que permiten agregar funcionalidades a Drupal.
# Creación (Drupal 8)
1. ## Estrucutra de carpetas
```
|--- modules/
|    |--- custom/
|        |--- Nombre_Modulo/
|             |--- src
|                  |--- Controller/
|                  |--- Form/
|                  |--- Plugin/
|                       |--- Block/
|             |--- templates       

```
# Creación de módulo basico
1. Crear una carpeta en la ruta module, que sera de la siguiente manera: custom/nombreModulo
2. Crear el archivo nombreModulo.info.yml con el siguiente contendio
```yml
name: Hello World Module
description: Creates a page showing "Hello World".
package: Custom
type: module
core: 8.x
#core_version_requirement: ^8 || ^9
dependencies:
  - drupal:link
  - drupal:views
  - paragraphs:paragraphs
  - webform:webform (>=8.x-5.x)

test_dependencies:
 - drupal:image

configure: hello.settings

php: 5.6

hidden: true
required: true

```
> - name: Nombre del módulo
> - description: Descripción del módulo
> - package: Permite agrupar módulos del mismo tipo
> - type: Indica el tipo de extensión, para este ejemplo module pero puede ser theme or profile
> - core: Especifica con cual core del drupal el módulo es compatible
> - core_version_requirement: Es importante dado que antes de la version 8.7.7 de drupal no reconoce el parametro core
> - dependencies: Es la lista de otros módulos de los cuales el tuyo depende
>   - {project}:{module} (>=8.x-5.x)
>       - project: Nombre del proyecto como aparece en drupal.org
>       - module: Nombre de la maquina del módulo
>       - (>=8.x-5.x): Los módulos también pueden incluir una restricción de versión, pero es opcional
> - test_dependencies: Lista de otros módulos que son necesarios para ejecutar test automaticos
> - configure: Si tu módulo dispone de una configuración, en este parámetro se especifica la ruta
> - php: Defini la mínima versión de php que requiere el módulo 
> - hidden: Ocultara el módulo de la lista de módulos en al pagina Extend
> - required: Indica que tu módulo debe estar habilitado  y no puede ser desinstalado
3.  Crear un archivo con el el nombre node.type.example_mytype.yml en la carpeta modules/customm/nombreModulo/config/install/ y agregar el siguiente código
```yml
langcode: en
status: true
dependencies: {  }
name: Article
type: article
description: 'Use <em>articles</em> for time-sensitive content like news, press releases or blog posts.'
help: ''
new_revision: true
preview_mode: 1
display_submitted: true
```
4. Crear configuracón por defecto para el módulo, en la carpeta modules/custom/nombreModulo/config/install/ agregar el archiov hello.settings.yml con el siguiente codigo
```yml
message: 'Hello'
langcode: 'en'
`
