# DynamoDb
# Despliegue en local
## 1. Descarga DynamoDb
En la siguiente url encontrara los link de descarga para las diferentes zonas [DynamoDB](https://docs.aws.amazon.com/es_es/amazondynamodb/latest/developerguide/DynamoDBLocal.DownloadingAndRunning.html)
## 2. Desplegar dynamoDB
Para desplegar DynamoDB debe tener las credenciales de un rol AIM de AWS y debe tener un JDK de java instalado.
Accede a la carpeta donde esta descomprimido la base de datos y ejecuta el siguiente comando 
```cmd
java -Djava.library.path=./DynamoDBLocal_lib -jar DynamoDBLocal.jar -sharedDb
```
## 3. Visualizar las tablas creadas
Para ello debera ejecutar el siguiente comando en cmd
```cmd
aws dynamodb list-tables --endpoint-url http://localhost:8000
```
