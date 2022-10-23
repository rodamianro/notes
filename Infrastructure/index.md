# Docker
Son entitades auto-contenidas que no pueden acceder al SO que lo esta ejecutando a menos que se lo permita
- Mientras el proceso principal de un contenedor esta corriendo, el contenedor seguira corriendo
## Manejo de archivos con docker
- 
# Docker de nginx
```sh
# Crea el contenedor de nginx
docker run -d --name proxy nginx
# Detienen el contenedor
docker stop proxy
# Eliminar un contenedor
docker rm proxy
# Eliminar un contenedor aunque este corriendo
docker rm -f proxy
# Crear un contenedor y que se exponga en un puerto
docker run --name proxy -p 8080:80 nginx
# Crear el contenedor y correrlo en segundo plano
docker run --name proxy -d -p 8080:80 nginx
# Ver los logs de un contenedor
docker logs proxy
# Ver los logs continuamente 
docker logs -f proxy
# Ver los ultimos logs
docker logs --tails 10 -f proxy
```
# Docker de mongo
```sh
# Crear el contenedor
docker run -d --name db mongo
# Acceder a la consola del contenedor
docker exec -ti db bash
# Acceso a archivos con bindmount
docker run -d --name db -v /home/develop/Documents/node/test/mongo_data:/data/db mongo
```
# Volumenes
```sh
# Ver los volumenes creados
docker volume ls
# Crear un volumen 
docker volume create dbdata
# Crea un contenedor indicandole el volumen
docker run -d --name db --mount src=dbdata,dst=/data/db mongo
# Ver información de un contenedor
docker inspect db
# Copiar archivos a un contenedor
docker cp prueba.tx  copytest:/testing/prueba.txt
# Extraer un archivo de un contenedor
docker cp copytest:/testing localtesting
```
