# MongoDB

## Primeros pasos:

 - El proyecto está montado sobre docker utilizando la imagen oficial de MongoDB alojada en dockerhub.
 - Montamos el proyecto mediante `docker-compose` y accedemos al contenedor de mongo

## Primeros comandos:

- `mongo` Para abrir la consola de MongoDB
  - `show dbs` Muestra un listado de bbdd alojadas en el servidor.
  - `use [databse_name]` Selecciona una bbdd para posteriormente trabajar sobre ella, si no existe se creará.
  - `show collections` Muestra el listado de colecciones dentro la bbdd seleccionada.
  - `db.[collection].find()` Muestra el listado de documentos dentro de la colección.
  - `db.[collection].find().pretty()` Similar al anterior, pero muestra el contenido de forma mas "amigable". 
  - `db.createCollection("[name]")` Para crear una nueva colección dentro de la bbdd.
  - `db.[collection].isert({jsonObject})` Para insertar dentro de la colección seleccionada.
  - Para modificar la información la sintaxis es como sigue: 
  ```
  db.[collection].update({
     [key]: 'value',
     },{$set: {[key]: 'newValue', [otherKey]: 'otherValue'}
  })
  ``` 
  - Si queremos actualizar añadiendo información al registro, la sintaxis es como sigue:
  ```
  db.[collection].update({
     [key]: 'value',
     },{$set: {[key]: 'newValue', [otherKey]: 'otherValue'}
  },{$upsert: true})
  ```
  - `db.[collection]`.remove({[key: value]})` Para eliminar un registro de la bbdd, si no se especificase ningún parámetro se eliminarian todos los documentos de la colección.
- `mongod`
- `mongosh`

## Consideraciones:

  MongoDB funciona como un intérprete de javascript por lo que podríamos ejecutar algo tal que así:
  
  ```javascript
    for (var i = 0; i < 10; i++) {db.things.insert({'x': i})}
  ```  

## Tipos de datos:

Existen seis tipos de datos fundamentales en MongoDB, seguidos de los mismos se muestra el valor típico de la clave que utiliza cada uno de ellos

- string
```javascript
{ name: 'john' }
```
- number
```javascript
{ likes: 5 }
```
- date
```javascript
{ timestamp:ISODate('...') }
```
- array
```javascript
{ tags: array } or {tags: []}
```
- boolean
```javascript
{ published: true }
```
- objectId
```javascript
{ _creator: Schema.ObjectId}
```

## Consultas 

Para realizar consultas se utiliza el comando `find()` como hemos visto arriba, éste puede recibir argumentos para filtrar los resultados.

```javascript
> db.[collection].find({key:value}) //devolverá los elementos de la colección cuya key sea igual a value
> db.[collection].find({key:{$gt: number}}) //devolverá los elementos de la colección cuya key sea mayor que el parámetro number.
> db.[collection].find({key:{$lt: number}}) //igual que el anterior pero en este caso los que sean menor que el parámetro number.
> db.[collection].find({key:{$in: ['value']}}) //El parámetro $in es específico para el tipo de datos array, devolverá aquellos elementos que contengan el parámetro value
```

### Ordenación

```javascript
> db.[collection].find().sort(key:1) //ordena por el parámetro key ascendentemente
> db.[collection].find().sort(key:-1) //ordena por el parámetro key descendentemente
```

### Número de resultados:

```javascript
> db.[collection].find().limit([number]) //Limita el resultado de la búsqueda al número especificado en el parámetro number
```

Se puede ver toda la documentación del lenguaje de consultas en el siguiente [enlace]

## Symfony & MongoDB

Para este proyecto de prueba se está utilizando un proyecto esqueleto de symfony al que se le han añadido varias dependencias como:

- `composer config "platform.ext-mongo" "1.6.16" && composer require alcaeus/mongo-php-adapter`
- `composer config extra.symfony.allow-contrib true`
- `composer require doctrine/mongodb-odm-bundle`
- `composer require --dev symfony/maker-bundle`
- `composer req validation`

Para crear el esquema de bbdd ejecutar el comando:

```
$ php bin/console doctrine:mongodb:schema:create
```

Se puede ver la documentación seguida en los siguientes enlaces:
- [Symfony4 y MongoDB]
- [Configurar MongoDB en Symfony]
- [Documentación MongoDBBundle]

[enlace]: <https://docs.mongodb.com/manual/>
[Symfony4 y MongoDB]: <https://medium.com/@ahmetmertsevinc/symfony-4-and-doctrine-mongo-db-c9ac0f02f742>
[Configurar MongoDB en Symfony]: <https://medium.com/francisco-ugalde/como-configurar-mongodb-en-symfony-4-d88e96f57aaa>
[Documentación MongoDBBundle]: <https://www.doctrine-project.org/projects/doctrine-mongodb-bundle/en/4.3/index.html>