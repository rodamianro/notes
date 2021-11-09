# Drupal
Apuntes sobre drupal

# Contenido
- [Drupal](#drupal)
- [Contenido](#contenido)
- [Arquitectura](#arquitectura)
  - [Núcleo](#núcleo)
  - [Modulos](#modulos)
  - [Área de administración](#área-de-administración)
  - [Nodos y tipos de contenido](#nodos-y-tipos-de-contenido)
  - [Entidades y campos](#entidades-y-campos)
  - [Menús](#menús)
  - [Bloques](#bloques)
  - [Temas](#temas)
  - [Usuarios, roles y permisos](#usuarios-roles-y-permisos)
  - [Taxonomía](#taxonomía)
  - [Estructura de archivos básica](#estructura-de-archivos-básica)
- [Trabajar en local](#trabajar-en-local)
  - [Desde pantheon](#desde-pantheon)
    - [Descargas](#descargas)
    - [Configuración inicial](#configuración-inicial)
- [Adicionales](#adicionales)
  - [Hooks](#hooks)

# Arquitectura
## Núcleo
Base necesaria para el funcionamiento y para la incorporación del resto de componentes de la arquitectura
## Modulos
Los módulos aportan funcionalidades adicionales al núcleo de Drupal
## Área de administración
El menú de administración se divice en grupos de tareas: Contendio, Estructura, Apariencia, Extender(Módulos), Configuración, Usuarios, Informes y Ayuda 
## Nodos y tipos de contenido
Los tipos de contendio en drupal derivan de un tipo de contenido básico denomindado <strong>nodo</strong>
## Entidades y campos
Las entidades son elementos a los que se les puede añadir campos de información de diferentes tipos, su propocito es homogeneizar la gestión y presentación de campos adicionales
## Menús 
Facilitan la organización de los nodos publicados
## Bloques
Son contendios principalmente dinámicos que se pueden habilitar en distintas zonas(regiones) del tema del sitio
## Temas
El tema define el diseño específico para el sitio web. Mediante el uso de temas, Drupal separa los contenidos del diseño.
Los temas se dividen en regiones, que son áreas diferenciadas en las que se puede colocar contenido
## Usuarios, roles y permisos
El control de acceso a las diferentes funcionalidades del sitio se realizan a través de los roles y permisos. Un rol es un conjunto de permisos.
## Taxonomía
Permite la clasificación de los contendios del sitio el módulo Taxonomy esta contruido por dos elementos: Los <strong>vocabularios</strong> (o categorías) y los <strong>términos</strong> (o etiquetas). Cada vocabulario puede agrupar a uno o más terminos.
## Estructura de archivos básica
```
|--- Proyecto_Drupal/
     |--- sites/
     |--- core/
     |--- modules/
          |--- contrib/
          |--- custom/
     |--- themes/
          |--- contrib/
          |--- custom/
```  
- ### sites/
    Se almacenan los datos de configuración del sitio y archivos
- ### core/
    Contiene los archivos del núcleo.
- ### modules/
    Se almacenan los módulos contrubuidos y los módulos personalizados
- ### themes/
    Se almacenan los temas contribuidos y los temas personalizados






# Trabajar en local
## Desde pantheon
### Descargas
1. Descargar la base de datos
2. Descargar el repositorio de codigo
3. Descargar los archivos sftp
### Configuración inicial
1. Instalar las dependencias con composer
```sh
$ composer install
```
2. Instalar drush (En caso de no estarlo ya)
```sh
$ composer require drush/drush
```
3. Crear archivo setting.local.php en la ruta default/ con minimo el siguiente código
```php
// Configuración de la base de datos
$databases['default']['default'] = [
    'database' => '',
    'username' => '',
    'password' => '',
    'host' => 'localhost',
    'port' => '3306',
    'driver' => 'mysql',
    'prefix' => '',
    'collation' => 'utf8mb4_general_ci',
];
// Hash-salt
$settings['hash_salt'] = '1';
```
4. Crear archivo service.local.yml en la ruta default/ y copiar el contendio del archivo default.services.yml y cambiar las siguientes lineas
```yml
debug: true
cache: false
```
5. En caso de no existir la carpeta config en la ruta default/, crearla
6. Ejecutar los comandos drush [(más información)](drush.md)
  ```sh
  $ vendor/bin/drush cr
  $ vendor/bin/drush updb
  ```
# Adicionales
## Hooks 
Permiten a los módulos interactura con el core de Drupal. [Más información](https://api.drupal.org/api/drupal/includes!module.inc/group/hooks/7.x)
