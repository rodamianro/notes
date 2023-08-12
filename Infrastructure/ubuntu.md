# Activar conexión SSH

1. Instalar el servicio SSH

    ```sh
    sudo apt install openssh-server
    ```

2. Comprobar estado y activar servidor SSH

    ```sh
    # Ver estado del servicio
    sudo systemctl status ssh
    # Habilitar el servicio
    sudo systemctl enable ssh
    # Iniciar el servicio
    sudo systemctl start ssh
    ```

3. Abrir el puerto SSH

    ```sh
    sudo ufw allow ssh
    ```

    > En caso de querer editar la configuración SSH se puede hacer en el archivo
    >
    > ```sh
    > sudo nano /etc/ssh/sshd_config
    > ```
    >
    > En caso realizar alguna modificación deberá reiniciar el servicio, para ello puede utilizar el siguiente comando
    >
    > ```sh
    > sudo service ssh restart
    > ```

4. Crear par de claves SSH

    ```sh
    # Crea la llave SSH
    ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
    # Inici el agente SSH
    eval "$(ssh-agent -s)"
    # Agregar la llave privada al agente
    ssh-add ~/.ssh/id_rsa
    ```

5. Copiar la clave pública al servidor

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

6. Conectarse mediante ssh

    ```sh
    ssh username@remote_host
    ```

7. Para utilizar la conexión remota desde Visual Studio Code puede seguir esta guia [DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-use-visual-studio-code-for-remote-development-via-the-remote-ssh-plugin-es)

## Connect to a new network in ubuntu server[[1]](https://www.dz-techs.com/es/connect-to-wifi-network-on-ubuntu-server)

1. Search the name of the network interface

   ```sh
   ls -l /sys/class/net
   ```

   this show the list of interfaces that you have in your pc

2. Search the network configuration file. This file is in the   folder /etc/netplan
3. Make a copy of the file 00-installer-config.yml and if you connection is by wifi make a copy too the file 00-installer-config.yml

   ```sh
   sudo cp 00-installer-config.yaml 00-installer-config.original.yaml
   sudo cp 00-installer-config-wifi.yaml 00-installer-config-wifi.original.yaml
   ```

4. Open the file that is about the interface that you will add the new network for instance:

    If you will add a new wifi network you has to update the file 00-installer-config-wifi.yaml with you favorite editor. This file has a structure like this:

    ```yaml
    # This is the network config written by 'subiquity'
    network:
        version: 2
        wifis:
            wlp1s0:
                access-points:
                    [NETWORK_NAME]:
                        password: [NETWORK_PASSWORD]
            dhcp4: true
    ```

5. Add your new network access into the config "access-point" following the structure like this:

   ```yaml
   # This is the network config written by 'subiquity'
    network:
        version: 2
        wifis:
            wlp1s0:
                access-points:
                    [NETWORK_NAME]:
                        password: [NETWORK_PASSWORD]
                    [NEW_NETWORK_NAME]:
                        password: [NEW_NETWORK_PASSWORD]
            dhcp4: true
   ```

   if I have a network called MY_NETWORK with the password MY_PASSWORD the file will be like this:

   ```yaml
   # This is the network config written by 'subiquity'
    network:
        version: 2
        wifis:
            wlp1s0:
                access-points:
                    MY_NETWORK:
                        password: MY_PASSWORD
            dhcp4: true
   ```

6. Save the changes and apply it:

    ```sh
    sudo netplan appy
    ```

## Utilities

### Laptop utility commands

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
  # IP address
  hostname -I | cut -d' ' -f1
  # Ports
  sudo lsof -i -P -n
  sudo lsof -i -P -n | grep LISTEN  
  ```

## References

* [Digital Guide IONOS](https://www.ionos.es/digitalguide/servidores/configuracion/ubuntu-ssh/)
* [DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-ubuntu-20-04-es)
* [GitHub Docs](https://docs.github.com/es/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent?platform=windows)
* [dz-techs.com](https://www.dz-techs.com/es/connect-to-wifi-network-on-ubuntu-server)
