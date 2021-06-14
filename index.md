## Introducción

Este es un resumen de comandos que he ido guardando durante mi aprendizaje y utilización de bases de datos en mongoDB. Espero que pueda seer de utilidad a otros como lo es para mí.

### Servicio Mongod


#### Ver si el servicio de Mongo está ejecutandose

```
 service mongod status
```
o sinó:

```
 sudo /etc/init.d/mongodb status
``` 

o sinó:
```
 systemctl status mongod
```

La salida debería ser algo como esto:

```
 ● mongod.service - MongoDB Database Server
     Loaded: loaded (/lib/systemd/system/mongod.service; disabled; vendor preset: enabled)
     Active: inactive (dead)
       Docs: https://docs.mongodb.org/manual
```
En este caso vemos que el servicio mongod se encuentra detenido.


#### Iniciar el servicio de Mongo

```
 service mongod start
```
o sinó:

```
 sudo /etc/init.d/mongodb start
``` 
o sinó:
```
 systemctl start mongod
```

#### Detener el servicio de Mongo

```
 service mongod stop
```
o sinó:

```
 sudo /etc/init.d/mongodb stop
``` 

o sinó:
```
 systemctl stop mongod
```

### Acceder a la consola

Si el demonio (servicio) de mongod se encuentra ejecutandose podemos acceder a la consola de mongo sencillamente escribiendo en la terminal:

```
 mongo
```

#### Acceder en caso de que la base de datos requiera autenticación

En caso de que a la base de datos se le haya aplicado autenticación debemos acceder introduciendo las credenciales correspondientes:

```
 mongo -username nombre_usuario -password contraseña_usuario
```
O de forma abreviada

```
 mongo -u nombre_usuario -p contraseña_usuario
```


### Acceder a una base de datos

Si ya tenemos una base de datos existente para poder utilizarla ejecutamos 

```
user NombreDB
```

Debemos mencionar que si la base de datos no existe con tan solo ejecutar el anterior comando estaremos creando la misma. Si agregamos documentos a dicha base de datos esta será guardada, pero si no se agrega ninguna colección o documentos a la misma dicha base de datos es eliminada automáticamente.

Para ver la base de datos actual:

```
 db
```


### Comando **show**

#### Ver bases de datos exitentes

```
 show dbs
```

#### Ver usuarios de mongo

Los usuarios se utilizan en el caso de que vayamos a implementar autenticación a alguna o algunas de nuestras bases de datos (Más adelante veremos como hacer eso). Con el siguiente comando podemos visualizar los usuarios que existan:

```
 show users
```

#### Ver colecciones existentes

Si ya nos encontramos dentro de una DB (hemos utilizado el comando use NombreDB), entonces podemos ver que colecciones existen dentro de dicha base de datos:

```
show collections
```

### Colecciones

#### Crear una colección

Creamos una colección llamada products.
```
 db.createCollection(“products”)
```

En Mongo no es obligatorio crear una colección de esta manera. Con el comando insert mostrado mas adelante también es posible crear la colección una vez que se agregan documentos a la misma.


#### Eliminar una colección

Eliminamos una colección llamada products.
```
 db.products.drop()
```

### Insertar documentos

Para insertar documentos dentro de una colección utilizamos **insert**

```
 db.products.insert({“name”: “Laptop DELL”})
```
En este caso hemos ejemplificado insertando el campo (field) **name** dentro de la colección **products**. En caso de que no exista dicha colección la misma es creada con la inserción del primer documento.


### Buscar documentos (find)

Para buscar documentos el comando básico es ***find*** y sus versiones. Por otra parte el comando ***aggregate*** permite realizar queries más complejas pero eso lo veremos más adelante.

Para ver todos los documentos de una colección:

```
 db.nombre_coleccion.find()
``` 

Si por otra parte queremos ver documentos específicos debemos ejecutar una query dentro del primer parámetro de find, por ejemplo, si desemos buscar un usuario de apellido "Gamez" dentro de la colección ***users*** ejecutamos la sentencia:

```
 db.users.find({lastName: "Gamez"}).pretty()
```

En el final hemos agregado el comando pretty(), el cuál mostrará la respuesta de una forma más amigable al usuario.

Si por otra parte utilizamos ***findOne*** obtenemos solo el primer documento como resultado de la query

```
 db.users.findOne({role: "student"}).pretty()
```

#### Mostrar determinado campos en la respuesta

Para esto definimos el segundo parámetro dentro del comando find:

```
 db.products.find({“name”: “Latitude”},{“name”:1})
```

#### Búsquedas condicionales

También podemos utilizar condicionales para realizar nuestras queries:

```
 db.users.find({age: {$gte: 25}}).pretty()
```
Es este caso hemos buscado todos los usuarios dentro de la colección users que tienen25 años o más. $gte nos retorna los documentos en cuyo campo que se compara se tenga un valor mayoe e igual a determinado valor. 

Tendremos entonces 
- $gt: mayores que ..., 
- $gte: mayores e iguales que ..., 
- $lt: menores que ..., 
- $lte: menores o iguales que ..., 


### Actualizar en múltiples documentos

Ejemplo: Para actualizar el valor del campo **fieldNameToUpdate** por el nuevo valor ***newValue***, en todos los documentos que cumplan con que el campo **fieldNameToSearch** tenga el valor ***value***.
```
 db.tx.updateMany({fieldNameToSearch: value},{$set: {fieldNameToUpdate: newValue}})
```

### Eliminar un documento

Si queremos eliminar un documento por ejemplo conociendo su "id" lo hacemos de la siguiente forma:
```
 db.paymentMethod.deleteOne({_id : ObjectId("6082fffb053c79232fbcf1bb")})
```


### Implementar Autenticación

...

#### Cambiar contraseña de la base de datos

```
 db.changeUserPassword(username, password)
```


### Exportar o Importar

#### Exportar con mongodump

Para exportar una base de datos completa utilizamos **mongodump**. Debemos tener en cuenta que debemos estar ubicados fuera de la consola de mongo, es decir, en una terminal normal. Nos ubicamos dentro de la carpeta donde queremos respaldar la base de datos y ejecutamos:

```
 mongodump --db nombre_bd
```
Donde hemos especificado el nombre de la base de datos que vamos a exportar. Una vez ejecutado el comando, Mongo va a crear una carpeta llamada dump, dentro de la ubicación donde nos encontrabamos en la consola cuando ejecutamos el comando. Dentro de dicha carpeta Mongo creará dos archivos por cada colección que tengamos.

#### Importar con mongorestore

Para importar una base de datos desde consola nos hubicamos en una carpeta que esté un nivel más arriba de la carpeta donde tengamos la DB que queremos importar y ejecutamos el comando:

```
  mongorestore --db nombre_que_se_dara_a_la_bd carpeta_donde_esta/
```

En el caso de una base de datos que requiere autenticación procedemos de la siguiente manera:

```
mongorestore --username username --password password --authenticationDatabase admin --db nombre_que_se_dara_a_la_bd carpeta_donde_esta/
```


### Indices

#### Indexar un campo

```
db.collection_name.createIndex({"campo_a_indexar": 1})
```
