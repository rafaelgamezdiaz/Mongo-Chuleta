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

### Implementar Autenticación

...

#### Cambiar contraseña de la base de datos

```
 db.changeUserPassword(username, password)
```

### Indices

#### Indexar un campo

```
db.collection_name.createIndex({"campo_a_indexar": 1})
```
