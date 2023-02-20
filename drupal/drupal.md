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
    - [Configuración inicial con lando](#configuración-inicial-con-lando)
- [Como Actualizar core de drupal con Composer](#como-actualizar-core-de-drupal-con-composer)
- [Configuración de estandares de programación en el entorno local](#configuración-de-estandares-de-programación-en-el-entorno-local)
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

Permite la clasificación de los contendios del sitio el módulo Taxonomy esta contruido por dos elementos: Los <strong>vocabularios</strong> (o categorías) y los <strong>términos</strong> (o etiquetas). Cada vocabulario puede agrupar a uno 
o más terminos.

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
3. Crear archivo settings.local.php en la ruta default/ con minimo el siguiente código
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
   3.1. Para un configuración más avanzada, copiar el contendio del archivo example.settings.local.php que se encuentran en la carpeta /sites, y descomentar las siguientes lineas:
   ```php
   $settings['cache']['bins']['render'] = 'cache.backend.null';
   $settings['cache']['bins']['discovery_migration'] = 'cache.backend.memory';
   $settings['cache']['bins']['page'] = 'cache.backend.null';
   $settings['cache']['bins']['dynamic_page_cache'] = 'cache.backend.null';
   ```
   Adicional debe agregar la configuración de la base de datos anteriormente mencionada, esta configuración permite realizar cambios en drupal y que estos se actualicen sin tener que utilizar drush cr
   3.2. Cambiar la ruta de las configuraciones por defecto
   ```php
   $settings['config_sync_directory'] = './config/sync/default';
   ```
4. Crear archivo services.local.yml en la ruta default/ y copiar el contendio del archivo default.services.yml y cambiar las siguientes lineas
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
### Configuración inicial con lando
Instalar proyecto: https://docs.lando.dev/getting-started/first-app.html
# Como Actualizar core de drupal con Composer

1.  Listar las actualizaciones disponibles para drupal
    ```sh
      $ composer outdated "drupal/*"
    ```
2. Verificar la versión de drupal que se usa
    ```sh
      $ composer show drupal/core-recommended
    ```
3. Descargar la versión de drupal recomendada
    ```
      $ composer update drupal/core "drupal/core-*" --with-all-dependencies
    ```
4. Actualizar la base de datos y limpiar la cache
    ```sh
      $ vendor/bin/drush cr
      $ vendor/bin/drush updb
    ```

# Configuración de estandares de programación en el entorno local

Para poder llevar un control de los estandares y lineamientos minimos esperados al programar modulos custom es recomendable utlizar las herramientas phpcs y phpcbf las cuales nos brindaran utilidades que podremos configurar que nos ayudara a tener siempre presente las buenas practicas y estandares esperados.

Para instalar estas dos herramientas los paso son:

1. Descargar la dependencia ya sea en un proyecto especifico o de manera global
   ```sh
   composer global require "squizlabs/php_codesniffer=*"
   ```
2. Actualizar el path que utilizara phpcs 
   ```cmd
   phpcs --config-set installed_paths C:\Users\[usuario_windows]\AppData\Roaming\Composer\vendor\drupal\coder\coder_sniffer
   ```
3. Instalar la guia de estilos de drupal
   ```sh
   composer global require drupal/coder
   ```
4. Comprobar guías de estilos instaladas
   ```sh
   phpcs -i
   ```
5. Configuración en visual studio code:
   Para que vscode hay que agregar la configuración correspondiente, para ello cree una carpeta con el nombre .vscode con un archivo json que tenga como nombre settings.json en la raiz del proyecto
   ```
   |-- .vscode/
       |-- settings.json
   ```
   Y agregue los siguiente atributos
   ```json
   {
    "phpcs.enable": true,
    "phpcs.executablePath": "C:/Users/USUARIO/AppData/Roaming/Composer/vendor/bin/phpcs.bat",
    "phpcs.standard": "Drupal,DrupalPractice",
    "phpcbf.enable": true,
    "phpcbf.documentFormattingProvider": true,
    "phpcbf.onsave": true,
    "phpcbf.standard": "Drupal,DrupalPractice",
    "phpcbf.executablePath": "C:/Users/USUARIO/AppData/Roaming/Composer/vendor/bin/phpcbf.bat"
   }
   ```
   Con ello configuraremos tanto phpcs y phpcbf para poder utilizar esas herramientas en vscode y que nos ayude a marcar los errores y a corregirlos.

   > Tener en cuenta la dirección de los ejecutables de ambas herramientas, ya que es importante que queden correctamente la ubicación de estas, ya sea que esten de forma global en nuestro equipo o que se encuentre dentro de un proyecto en especifico

# Adicionales

## Hooks 

Permiten a los módulos interactura con el core de Drupal. [Más información](https://api.drupal.org/api/drupal/includes!module.inc/group/hooks/7.x)
