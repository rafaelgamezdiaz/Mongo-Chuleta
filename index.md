## Mongo-Chuleta

Este es un resumen de comandos que he ido guardando durante mi aprendizaje y utilización de bases de datos en mongoDB. Espero que pueda seer de utilidad a otros como lo es para mí.

### Implementar Autenticación

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

#### Cambiar contraseña de la base de datos

```
 db.changeUserPassword(username, password)
```

### Indices

#### Indexar un campo

```
db.collection_name.createIndex({"campo_a_indexar": 1})
```
