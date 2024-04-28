# MongoDB

## Tabla de contendio

- [MongoDB](#mongodb)
  - [Tabla de contendio](#tabla-de-contendio)
  - [Definition](#definition)
  - [MongoDB Atlas](#mongodb-atlas)
  - [Definiciones generales](#definiciones-generales)
  - [Base de datos](#base-de-datos)
  - [Colecciones](#colecciones)
  - [Documentos](#documentos)
  - [JSON VS BSON](#json-vs-bson)
    - [JSON](#json)
    - [BSON](#bson)
  - [Operations](#operations)
- [Tipos de datos](#tipos-de-datos)
- [Esquemas](#esquemas)
- [Relaciones](#relaciones)
- [Operadores](#operadores)
  - [Operadores de Compraración](#operadores-de-compraración)
  - [Operadores de lógicos](#operadores-de-lógicos)
  - [Operadores por elemento](#operadores-por-elemento)
  - [Operadores para arreglos](#operadores-para-arreglos)
  - [Operadores para realizar Updates en arreglos](#operadores-para-realizar-updates-en-arreglos)
- [Proyecciones](#proyecciones)
  - [Exportar una base de datos](#exportar-una-base-de-datos)
  - [Restaurar base de datos](#restaurar-base-de-datos)

## Definition

Es una base de datos no relacional basada en documentos.

- Permite guardar estructuras tipo json (BSON)
- Base de datos distribuida
- Se puede escalar de forma horizontal
- Es schema less, se pueden guardar docuemtos que no necesariamente tenga la misma estructura
- Es de código abierto y gratis

## MongoDB Atlas

- Aprovisionamiento automático de clusters con MongoDB
- Alta disponibilidad
- Altamente escalable
- Seguro
- Disponible en AWS, GCP y Azure
- Fácil monitoreo y optimización

## Definiciones generales

## Base de datos

- Es un contennedor físico de colecciones
- Cada base de datos tiene su archivo propio en el sistema de archivos
- Un cluster puede tener múltiples bases de datos

## Colecciones

- Agrupación de documentos
- Equivalente a una tabla en las bases de datos relacionales
- No impone un esquema

## Documentos

- Un registro dentro de una colección
- Es análogo a un objeto JSON(BSON)
- La unidad básica dentro de MongoDB

## JSON VS BSON

### JSON

```json
{
    "name": "Some name",
    "age": 30,
    "nickName": "nickName"
}
```

### BSON

Codificación binaria de documentos JSON

## Operations

- Crear base de datos:
  
    ```js
    use 'nombreDB'
    ```

- .insertOne(): Insertar un elemento
  
    ```js
    db.inventory.insertOne(
    { item: "canvas", qty: 100, tags: ["cotton"], size: { h: 28, w: 35.5, uom: "cm" } })
    ```
* .insertMany(): Insertar varios elementos
    ```js
    db.inventory.insertMany( [
   { item: "canvas", qty: 100, size: { h: 28, w: 35.5, uom: "cm" }, status: "A" },
   { item: "journal", qty: 25, size: { h: 14, w: 21, uom: "cm" }, status: "A" },
   { item: "mat", qty: 85, size: { h: 27.9, w: 35.5, uom: "cm" }, status: "A" },
   { item: "mousepad", qty: 25, size: { h: 19, w: 22.85, uom: "cm" }, status: "P" },
   { item: "notebook", qty: 50, size: { h: 8.5, w: 11, uom: "in" }, status: "P" },
   { item: "paper", qty: 100, size: { h: 8.5, w: 11, uom: "in" }, status: "D" },
   { item: "planner", qty: 75, size: { h: 22.85, w: 30, uom: "cm" }, status: "D" },
   { item: "postcard", qty: 45, size: { h: 10, w: 15.25, uom: "cm" }, status: "A" },
   { item: "sketchbook", qty: 80, size: { h: 14, w: 21, uom: "cm" }, status: "A" },
   { item: "sketch pad", qty: 95, size: { h: 22.85, w: 30.5, uom: "cm" }, status: "A" }
    ] )
    ```
* .help(): Ver comandos que se pueden ejecutar sobre la colección
    ```js
    db.inventory.help()
    ```
* .find(): Buscar todos los documentos que cumplan la condición
    ```js
    db.inventory.find({item:"canvas"})
    ```
* .pretty(): Muestra el resultado en consola de forma más "bonita"
    ```js
    db.inventory.find({item:"canvas"}).pretty()
    ```
* .count(): Contar los elementos que retorna una consulta
    ```js
    db.inventory.find({item:"canvas"}).count()
    ```
* .findOne(): Devuelve un documento por orden natural
    ```js
    db.inventory.findOne()
    ```
* .findOne({}): Devuelve un documento por orden natural
    ```js
    db.inventory.findOne({ _id: ObjectId('6258c94f8e97c6326e125ca9')})
    ```
* .updateOne(): Actualizar un documento
    ```js
    db.inventory.updateOne({ _id: ObjectId('6258c94f8e97c6326e125ca9')}, {$set: {qty:130}})
    ```
* .updateMany(): Actualizar los docuemtos que cumpla la condición
    ```js
    db.inventory.updateMany({ item: 'canvas'}, {$set: {qty:130}})
    ```
* .deleteOne(): Eliman el primer documento en orden natural que cumpla la condición
    ```js
    db.inventory.deleteOne({ status: 'A'})
    ```
* .deleteMany(): Eliman el primer documento en orden natural que cumpla la condición
    ```js
    db.inventory.deleteOne({ status: 'A'})
    ```
* .limit(): Retorna la cantidad de elementos indicada
    ```js
    db.carreras.find({}).limit(10)
    ```
* .skip(): Deja como valor inicial de la consulta el que se encuentre en la posición indicada
    ```js
    db.carreras.find({}).skip(40).limit(10)
    ```
# Tipos de datos
- Strings: Sirven para guardar texto
- Boolean: True|False
- ObjectId: Existen en BSON y son unicos ObjectId("5sc...")
- Date: Permiten guardar fechas en los documentos ISODate("2019-02-18T...")
- Number:
  - Double: Guardar información que tenga punto decimal
  - Integer 32 Bits: Guardar información entera
  - Integer 64 Bits: Guardar información entera
  - Decimal: Guardar información cuando se tienen muchos millones
- Documentos embebidos: Permite agregar documentos dentro de otros
- Arreglos: Pueden ser de cualquiera de los tipos de datos
# Esquemas
Forma en la que organizamos nuestros documentos
# Relaciones
Son la forma en la que las entidades se encuentran enlazados unos con otros
* ## Uno a uno
    Para las relaciones Uno a uno creamos documentos embebidos
* ## Uno a muchos
    Se crea un referencia en la coleción de la parte muchos
# Operadores
La forma de agregar operadores en un filtro es:
```json
{<field1>}: {<operator1>: { <value1>}}
```
Ejemplo:
```js
db.inventory.find({status:{$in:["A","D"]},...})
```
## Operadores de Compraración
| Nombre | Descripcion                                |
| ------ | ------------------------------------------ |
| $eq    | =                                          |
| $gt    | >                                          |
| $gte   | >=                                         |
| $lt    | <                                          |
| $lte   | <=                                         |
| $ne    | !=                                         |
| $in    | Valores dentro de un arreglo               |
| $nin   | Valoques que no están dentro de un arreglo |
## Operadores de lógicos
| Nombre | Descripcion                   |
| ------ | ----------------------------- |
| $and   | Une queries con un and lógico |
| $not   | Invierte el efecto del query  |
| $nor   | Une queries con un nor lógico |
| $or    | Une queries con un or lógico  |
## Operadores por elemento
| Nombre | Descripcion                                             |
| ------ | ------------------------------------------------------- |
| $exist | Documentos que cuentan con un campo especifico          |
| $type  | Documentos que cuentan con un campo del tipo especifico |
## Operadores para arreglos
| Nombre     | Descripcion                                                                |
| ---------- | -------------------------------------------------------------------------- |
| $all       | Arreglos que contengan todos los elementos del query                       |
| $elemMatch | Documentos que cumplen la condición del $elemMatch en uno de uss elementos |
| $size      | Documentos que contienen un campo tipo arreglo de un tamaño especifico     |
## Operadores para realizar Updates en arreglos
| Nombre    | Descripcion                      |
| --------- | -------------------------------- |
| $addToSet | Agrega unobjeto al arreglo       |
| $pull     | Retira un elemento de un arreglo |
# Proyecciones
Permite mostrar cierta información de los documentos que se consultan
```js
db.inventory.findOne({status: "A"}, {item:1, status:1})
```
se usa 1 para indicar que lo traiga y 0 en caso contrario

## Exportar una base de datos

```sh
mongodump --uri="[mongo_server_url]" --db [mongo_db_name] --out=[output_url]
```

## Restaurar base de datos

```sh
mongorestore -u [user] -p [password] --authenticationDatabase=admin ---host=[mongo_server_url] --port=[mongo_server_port] --db=[db_name] [backup_url]
```
