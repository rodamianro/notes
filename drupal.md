# Drupal
Apuntes sobre drupal

# Contenido
- [Drupal](#drupal)
- [Contenido](#contenido)
- [Consideraciones al crear código para drupal](#consideraciones-al-crear-código-para-drupal)
  - [Patrones de diseño](#patrones-de-diseño)
    - [1. Factory](#1-factory)
    - [2. Singleton](#2-singleton)
  - [3. Strategy](#3-strategy)
    - [Front Controller](#front-controller)

# Consideraciones al crear código para drupal

## Patrones de diseño

### 1. Factory
Se crea una clase que solo cree el objeto que se quiere usar, esto permite que dado el caso que se tenga que cambiar la clase Automobile, solo se haga en la clase Factory, otro beneficio podria ser al momento de que la creación de una clase se un trabajo complicado, se puede delegar este trabajo a la clase fatory
```php
<?php
class Automobile
{
    private $vehicleMake;
    private $vehicleModel;

    public function __construct($make, $model)
    {
        $this->vehicleMake = $make;
        $this->vehicleModel = $model;
    }

    public function getMakeAndModel()
    {
        return $this->vehicleMake . ' ' . $this->vehicleModel;
    }
}

class AutomobileFactory
{
    public static function create($make, $model)
    {
        return new Automobile($make, $model);
    }
}

// have the factory create the Automobile object
$veyron = AutomobileFactory::create('Bugatti', 'Veyron');

print_r($veyron->getMakeAndModel()); // outputs "Bugatti Veyron"
```
### 2. Singleton
El patron singleton es util cuando necesitamos asegurarnos de tener una unica instancia de una clase unicamente para manejar el ciclo completo de peticiones en una aplicación web
```php
<?php
class Singleton
{
    private static $instance = null;

    private function __construct() {}

    public static function getInstance(): self
    {
        if (null === self::$instance) {
            self::$instance = new self();
        }

        return self::$instance;
    }
}
```
## 3. Strategy
Con el patron strategy puedes encapsular conjuntos especificos de algoritmos haciendo a la clase cliente la responsable por la instaciacion de un algoritmo en particular sin tener conocimiento de su actual implementación
```php
<?php
interface OutputInterface
{
    public function load();
}

class SerializedArrayOutput implements OutputInterface
{
    public function load()
    {
        return serialize($arrayOfData);
    }
}

class JsonStringOutput implements OutputInterface
{
    public function load()
    {
        return json_encode($arrayOfData);
    }
}

class ArrayOutput implements OutputInterface
{
    public function load()
    {
        return $arrayOfData;
    }
}
``` 
Encapsulando los algoritmos los hace mas faciles y claros en tu código para que otros desarrolladores puedan facilmente agregar tipo de outputs sin afectar el código del cliente.
Veras como en cada clase output en concreto implementa una OutputInterface, esto sirve para 2 propositos.

1. Proveer un contrato simple el cual debe ser obedecido por cualquie nueva implementación.
2. Por la implementación de una interfaz común te aseguras que las acciones del cliente sean del tipo correcto

```php
<?php
class SomeClient
{
    private $output;

    public function setOutput(OutputInterface $outputType)
    {
        $this->output = $outputType;
    }

    public function loadOutput()
    {
        return $this->output->load();
    }
}

$client = new SomeClient();

// Want an array?
$client->setOutput(new ArrayOutput());
$data = $client->loadOutput();

// Want some JSON?
$client->setOutput(new JsonStringOutput());
$data = $client->loadOutput();
```
### Front Controller 
El patron front Controller se utiliza cuando se tiene un unico punto de entrada a la aplicación web, este maneja todas las peticiones. Este código es responsable por la carga de todas las dependencias, procesamiento de peticiones y envio de respuestas al navegador. Este patron puede ser beneficioso porque fomenta el codigo modular y brinda lugar central donde se conecta el codigo que debe ejecutar cada petición
