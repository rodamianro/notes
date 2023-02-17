# Activar conexión SSH

1.  Instalar el servicio SSH    
    ```sh
    sudo apt install openssh-server
    ```
2.  Comprobar estado y activar servidor SSH
    ```sh
    # Ver estado del servicio
    sudo systemctl status ssh
    # Habilitar el servicio
    sudo systemctl enable ssh
    # Iniciar el servicio
    sudo systemctl start ssh
    ```
3.  Abrir el puerto SSH
    ```sh
    sudo ufw allow ssh
    ```
> En caso de querer editar la configuración SSH se puede hacer en el archivo
> ```sh
> sudo nano /etc/ssh/sshd_config
> ```
> En caso realizar alguna modificación deberá reiniciar el servicio, para ello puede utilizar el siguiente comando
> ```sh
> sudo service ssh restart
> ```
1.  Crear par de claves SSH
    ```sh
    # Crea la llave SSH
    ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
    # Inici el agente SSH
    eval "$(ssh-agent -s)"
    # Agregar la llave privada al agente
    ssh-add ~/.ssh/id_rsa
    ```
2.  Copiar la clave pública al servidor
    ```sh
    # Muestra en consola el contenido de la llave
    cat ~/.ssh/id_rsa.pub
    ```
    Copiamos el contenido de la llave publica y lo pegamos en
    ```sh
    # Agrega al archivo authorized_keys el texto de la llave pública
    echo public_key_string >> ~/.ssh/authorized_keys
    # Dar los permisos necesarios a la carpeta .ssh
    chmod -R go= ~/.shh
    # Da la propiedad de la carpeta ssh al usuario que la vaya a utilizar
    chown -R user:user ~/.ssh
    ```
3.  Conectarse mediante ssh
    ```sh
    ssh username@remote_host
    ```
4.  Para utilizar la conexión remota desde Visual Studio Code puede seguir esta guia [DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-use-visual-studio-code-for-remote-development-via-the-remote-ssh-plugin-es)
# Utilities

## Laptop utility commands
* Manage the laptop screen
  ```sh
  # Install  vbetool
  sudo apt intall vbetool
  # Turn off screen
  sudo vbetool dpms off
  # Turn on screen
  sudo vbetool dpms on
  ``` 
  > If you turn off the screen and then turn it on, the terminal doesn't show itself, be carefu
* General management
  ```sh 
  # Battery status
  acpi -i -b
  ```
# References

* [Digital Guide IONOS](https://www.ionos.es/digitalguide/servidores/configuracion/ubuntu-ssh/)
* [DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-ubuntu-20-04-es)
* [GitHub Docs](https://docs.github.com/es/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent?platform=windows)