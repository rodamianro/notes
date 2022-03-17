# Módulos en Drupal
Son elementos que permiten agregar funcionalidades a Drupal.
# Creación (Drupal 8) [[1]](https://www.drupal.org/docs/creating-custom-modules)
1. ## Estrucutra de carpetas
```
|--- modules/
|    |--- custom/
|        |--- nombre_modulo/
|             |--- src/
|                  |--- Controller/
|                  |--- Form/
|                  |--- Plugin/
|                       |--- Block/
|             |--- templates       

```
# Módulo basico
## 1.  custom/nombre_modulo: 
La creación del módulo empieza eligiendo el nombre de maquina del módulo que para este caso es nombre_modulo y creando una carpeta en al ruta modules/custom/nombre_modulo

## 2. nombre_modulo.info.yml: 
Es parte escencial de los modulos, temas o perfiles de instalación de drupal ya que almacenan los metadatos sobre el proyecto.

Este archivo es requerido para:
- Notificar a drupal sobre la existencia de un modulo, tema o perfil de instalación
- Provee información para la web UI de administración de drupa
- Provee criterios de control, activación y desactivación para el módulo como tambien la versión de drupal compatible

```yml
name: Hello World Module
description: Creates a page showing "Hello World".
package: Custom
type: module
core: 8.x
```
> - name: Nombre del módulo
> - description: Descripción del módulo
> - package: Permite agrupar módulos del mismo tipo
> - type: Indica el tipo de extensión, para este ejemplo module pero puede ser theme or profile
> - core: Especifica con cual core del drupal el módulo es compatible
> - core_version_requirement: Es importante dado que antes de la version 8.7.7 de drupal no reconoce el parametro core
> - [Más información sobre .info.yml](https://www.drupal.org/docs/creating-custom-modules/let-drupal-know-about-your-module-with-an-infoyml-file)
## 3. Creando una pagina personalizada [[2]](https://www.drupal.org/docs/creating-custom-modules/create-a-custom-page)
En primer lugar necesitas declarar la ruta en nombre_modulo.routing.yml, además necesitaras agregar un controller que retorne el cuerpo de la pagina
- ## Declarando una ruta
  La informacion de routing se almacena en nombre_modulo/nombre_modulo.routing.yml
  ```yml
  nombre_modulo.page:
    path: '/page'
    defaults:
      _controller: '\Drupal\nombre_modulo\Controller\NombreModuloController::page'
      _title: 'Pagina del módulo de prueba'
    requirements:
      _permission: 'access content'
  ```
  > - nombre_modulo.page: Es el nombre de máquina de la ruta. Por convención, este debe ser nombre_modulo.sub_name
  > - path: Da la url a la pagina en tu sitio
  > - defaults: Describe la pagina y el título
  > - requirements: Condiciones bajo las cuales la pagina debe ser mostrada. Puedes especificar permisos, módulos que serán habilitados, y otras condiciones
- ## Agregando un controlador
  El controlador retorna el cuerpo de página, debe ser un método de clase o un servicio registrado. Puede ser diferente dependiendo de varias condiciones.

  La clase controlador debe ser definida en nombre_modulo/src/Controller/NombreModuloController.php
  ```php
  <?php
  namespace Drupal\example\Controller;

  use Drupal\Core\Controller\ControllerBase;

  /**
  * Provides route responses for the Example module.
  */
  class ExampleController extends ControllerBase {

    /**
    * Returns a simple page.
    *
    * @return array
    *   A simple renderable array.
    */
    public function page() {
      return [
        '#markup' => 'Hola, mundo',
      ];
    }

  }
  ```
  > - namespace: Es necesario declarar el prefijo para clasificar completamente el nombre de la clase que estamos definiendo
  > - use: Nos permite utilizar ControllerBase en lugar del nombre completo
  > - page: El método especificado en el YAML debe ser publico. Debe retornar un array renderizable

# Generalidades 
## Array de renderizado [[2]](https://api.drupal.org/api/drupal/core!lib!Drupal!Core!Render!theme.api.php/group/theme_render/8.2.x)
Es un bloque de contrucción de pagina de drupal. Es un array asociativo jerárquico que contiene la información y las propiedades que describen como estas deben ser renderizada.

Cada nivel de jerárquia de un array de renderizado tiene uno o mas arrays de elementos. Los nombres de los arrays de elementos que empiezan con **#** son conocidos como "propiedades", y los arrays de elementos con otros nombres son "hijos"; Los nombres de los hijos son más flexibles, mientras que los nombres de las propiedades son especificos del Render API y el tipo particular de información que se esta procesando. Un caso especial de array de renderizado es el array para formulario, el cual especifica los elementos del formulario para un formulario HTML. <u>[Ver más](https://api.drupal.org/api/drupal/core%21core.api.php/group/form_api/8.2.x)</u>

Los arrays de renderizado suelen tener una de las siguientes propiedades definidas:
- \#type: Especifica la información del contendio y las opciones particulares del tipo de elemento a renderzar (form, textfield, submit, table)
- \#theme: Especifica la información a la cual se le aplicara un tema por un hook de tema especifico. Los módulos definen los hooks theme mediante la implementación de [hook_theme()](https://api.drupal.org/api/drupal/core%21lib%21Drupal%21Core%21Render%21theme.api.php/function/hook_theme/8.2.x), el cual especifica las variables de entrada usadas para proveer la información y las opciones.
- \#markup: Especifica un array que provee HTML directamente
- \#plaint_text: Especifica un array que provee texto
```php
  $output['admin_filtered_string'] = [
    '#markup' => '<em>This is filtered using the admin tag list</em>',
  ];
  $output['filtered_string'] = [
    '#markup' => '<video><source src="v.webm" type="video/webm"></video>',
    '#allowed_tags' => [
      'video',
      'source',
    ],
  ];
  $output['escaped_string'] = [
    '#plain_text' => '<em>This is escaped</em>',
  ];
``` 
   
  


