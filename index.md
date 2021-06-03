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


### Utilizar una base de datos

Si ya tenemos una base de datos existente para poder utilizarla ejecutamos 

```
user NombreDB
```

Debemos mencionar que si la base de datos no existe con tan solo ejecutar el anterior comando estaremos creando la misma. Si agregamos documentos a dicha base de datos esta será guardada, pero si no se agrega ninguna colección o documentos a la misma dicha base de datos es eliminada automáticamente.


### Comandos para visualizar

#### Ver bases de datos exitentes

```
 show dbs
```

#### Ver usuarios de mongo

Los usuarios se utilizan en el caso de que vayamos a implementar autenticación a alguna o algunas de nuestras bases de datos (Más adelante veremos como hacer eso). Con el siguiente comando podemos visualizar los usuarios que existan:

```
 show users
```

#### Ver colexiones existentes

Si ya nos encontramos dentro de una DB (hemos utilizado el comando use NombreDB), entonces podemos ver que colecciones existen dentro de dicha base de datos:

```
show collections
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


### Exportar o Importar una base de datos

