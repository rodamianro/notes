# Wordpress

## Custom themes

1. Create the folder for your theme in the following path: wp-content/themes

    ```folder
    |--- wp-content
        |--- themes
              |--- custom-theme-name
    ```

2. The theme minimum requires of two files: the index.php file and a style.css

    ```folder
    |--- wp-content
         |--- themes
              |--- custom-theme-name
                   |--- index.php
                   |--- style.css
    ```

3. To activate the theme you need to configure it in the style.css file

    ```css
    /*
    Theme Name: Custom theme
    Author: Theme Author 
    Author URI: Theme Author uri
    Description: Theme description
    Requires at least: 6.1
    Tested up to: 6.2
    Requires PHP: 5.6
    Version: 1.0
    License: GNU General Public License v2 or later
    License URI: https://www.gnu.org/licenses/old-licenses/gpl-2.0.html
    Text Domain: Theme text domain
    /
    ```

## Fixes

### Windows

* localwp doesn't route the wordpress site because the port 80 is in use

    ```cmd
    # Stop the process that it's using the port 80
    net stop http
    ```

    Then you will be enable to run a new process in this port, after that you can enable the http service again

    ```cmd
    # Start the service http
    net start http
    ```

    > You must execute the command in a terminal with admin permission