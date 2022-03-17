# Api Rest
Recursos rest creados en drupal
# Creación (Drupal 9)
## 1. Estructura
```
|--- web/modules/
|    |--- custom/
|        |--- api_rest/
|             |--- config/
|                  |--- install/
|             |--- src/
|                  |--- Normalizer/
|                  |--- Services/
|                  |--- Plugin/
|                       |--- rest/
|                            |--- resource/
```
## 2. Archivos de configuración
### 2.1. Creación de info.yml
Almacena los metadatos del módulo, se crea en la raiz del módulo
```yml
name: Api Rest
description: Define recursos rest personalizados 
package: custom
type: module
core: 9.x
```
### 2.2. Creación del .module
Almacena las configuraciónes de los hooks, se guarda en la raiz del módulo
### 2.3.  Creación del .services.yml
Almacena y permite el acceso a los diferentes servicios del módulo, se guarda en la raiz del módulo
### 2.4. Ejemplo 
```
|--- api_rest/
|    |--- api_rest.info.yml
|    |--- api_rest.services.yml
|    |--- api_rest.module
```
## 3. Creación de un recurso rest
### 3.1. Creación del recurso
En la carpeta resource se crear un archivo .php con el nombre; para este ejemplo Content el cual ayuda a identificar para que sirve el recurso seguida de la palabra resource, como se ve a continuación
```
|--- Plugin/rest/resource
|    |--- ContentResource.php
```
La base de esta clase sera la siguiente
```php
<?php
// Namespace de la clase
namespace Drupal\api_rest\Plugin\rest\resource;

// Sirve para crear el recurso
use Drupal\rest\Plugin\ResourceBase;
// Sirve para retornar una respuesta
use Drupal\rest\ResourceResponse;

/**
 * @RestResource(
 *  id = "content_resource",
 *  label = @Translation("Content Resource"),
 *  uri_paths = {
 *      "canonical" = "/api/content_resource/{id}"
 *  }
 * )
 */
class ContentResource extends ResourceBase
{
    /**
     * Obtienen el la información de un contenido
     */
    public function get($id)
    {
        $node = Node::load($id);
        return new ResourceResponse($node);
    }
}
```
