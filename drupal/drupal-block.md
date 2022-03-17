# Bloques en drupal
Contenedores que permiten colocar información en cualquier región de un tema
## Estrucutura
Los bloques se crean en la carpeta block
```
|--- modules/
|    |--- custom/
|        |--- nombre_modulo/
|             |--- src/
|                  |--- Plugin/
|                       |--- Block/
```
## Creación de archivo para el bloque
Por norma este terminar con Block al final del nombre por ejemplo HelloBlock.php
```
|--- src/Plugin/Block/
|    |--- HelloBlock.php      
```
## Estructura del archivo
```php
<?php

namespace Drupal\hello_world\Plugin\Block;

use Drupal\Core\Block\BlockBase;

/**
 * Provides a 'Hello' Block.
 *
 * @Block(
 *   id = "hello_block",
 *   admin_label = @Translation("Hello block"),
 *   category = @Translation("Hello World"),
 * )
 */
class HelloBlock extends BlockBase {

  /**
   * {@inheritdoc}
   */
  public function build() {
    return [
      '#markup' => $this->t('Hello, World!'),
    ];
  }

}
```
### @Block
Es la anotación que determina que la clase es un bloque, y le indica a drupal las caracteristicas de este. Los atributos basícos para esta son
```php
/**
 * Provides a 'Hello' Block.
 *
 * @Block(
 *   id = "hello_block",
 *   admin_label = @Translation("Hello block"),
 *   category = @Translation("Hello World"),
 * )
 */
class HelloBlock extends BlockBase {}
```
> * id:Identificador del bloque
> * admin_label: Nombre con el que se mostrar en la pagina de administración de bloques
> * category: Descripción del bloque
### BlockBase
Clase base para la definición de un bloque, contiene los métodos basícos para la creación de un bloque
```php
class HelloBlock extends BlockBase {}
```
### build()
Función obligatoria para la construción del bloque, esta función contiene la logica del bloque, retorna un array de renderizado
```php
class HelloBlock extends BlockBase {
  /**
   * {@inheritdoc}
   */
  public function build() {
    return [
      '#markup' => $this->t('Hello, World!'),
    ];
  }
}

```
## Uso de tema en el bloque
Para poder usar un tema en un bloque, se debe crea un templete Twig para ello seguir los pasos de creación de un [Templates en módulo personalizado](/drupal-twig.md), después de esto indicamos el bloque cúal tema debe utilizar
```php
class HelloBlock extends BlockBase {
  /**
   * {@inheritdoc}
   */
 public function build() {
    return [
      '#theme' => 'hello_base',
      '#data' => ['age' => '31', 'DOB' => '2 May 2000'],
    ];
  }
}
```
