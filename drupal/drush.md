# Drush

Es un shell de linea de comandos y una interfaz de scripting Unix para Drupal

# Comandos Utiles

- ## cr (cache-rebuild)

    Limpia el cache de Drush y los caches de renderización de Drupal
    ```sh
    $ drush cr
    ```

- ## updb(updatedb)
  
    Aplica todas las actualizaciones requeridas por la base de datos
    ```sh
    $ drush updb
    ```

- ## cex (config-export)

    Exporta los archivos de configuración del sitio al directorio config
    ```sh
    $ drush cex
    ```

- ## cim (config-import)
    Importa la configuración que se encuentra en la carpeta config
    ```
    $ drush cim
    ```

- ## config-delete nombre.configuracion

    Elimina una configuración especifica
    ```
    $ drush config-delete nombre.configuracion
    ```
- ## uli (user-login)

    Genera un link unico de logueo
    ```
    $ drush uli
    ```

> Puede ver todos los comando que tiene drush los puede encontrar en [Drush Commands](https://drushcommands.com/) 

> Fix: Cuando no carguen los estilos:
> 
> * drush -y config-set system.performance css.preprocess 0
> * drush -y config-set system.performance js.preprocess 0