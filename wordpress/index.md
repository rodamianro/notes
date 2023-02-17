# Wordpress
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