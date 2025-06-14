# MongoDB-queries-from-terminal

Ejercicios NoSQL & MongoDB
🎯 Objetivos:

Comprender qué es una base de datos no relacional.
Comprender cómo se realizan las consultas a una base de datos no relacional.
Analizar y diseñar bases de datos con sus correspondientes colecciones.
Comprender cómo interactuar con los datos almacenados en la base de datos.



##1. Desarrollar el Proyecto
A continuación, creará su propia base de datos de red social con las siguientes colecciones:

users
posts

SOLUCIÓN: 
```js
use ejercicioRedSocial
db.createCollection("users")
db.createCollection("posts")
```

##2. Ejecute las siguientes consulta
A continuación tendrás que realizar las siguientes consultas MongoDB:


##2.1 INSERTAR DATOS
Insertar al menos 15 publicaciones nuevas con al menos 2 comentarios por publicación:

title
body
username
comments
	username
	body

SOLUCIÓN: 
```js
db.posts.insertOne ({
	title:"Título post 1",
	body: "Contenido post 1",
	username: "Creadora contenido 1",
	comment: {
		username:"comentadora 1",
 		body:"contenido Comentario 1"}
})

db.posts.insertMany ([

{
     title: "Título post 2",
     body: "Contenido post 2",
     username: "Creadora contenido 2",
     comment: {
         username: "comentadora 2",
         body: "contenido Comentario 2"
     }
 },

 {
     title: "Título post 3",
     body: "Contenido post 3",
     username: "Creadora contenido 3",
     comment: {
         username: "comentadora 3",
         body: "contenido Comentario 3"
     }
 },

 {
     title: "Título post 4",
     body: "Contenido post 4",
     username: "Creadora contenido 4",
     comment: {
         username: "comentadora 4",
         body: "contenido Comentario 4"
     }
 } 

])
```

Insertar al menos 10 nuevos usuarios:


username
email
age

SOLUCIÓN: 
```js
db.users.insertMany([
...   { username: "Creadora contenido 1", email: "creadora1@email.com", age: 28 },
...   { username: "Creadora contenido 2", email: "creadora2@email.com", age: 30 },
...   { username: "Creadora contenido 3", email: "creadora3@email.com", age: 25 },
...   { username: "Creadora contenido 4", email: "creadora4@email.com", age: 32 },
...   { username: "Creadora contenido 5", email: "creadora5@email.com", age: 27 },
...   { username: "Creadora contenido 6", email: "creadora6@email.com", age: 31 },
...   { username: "Creadora contenido 7", email: "creadora7@email.com", age: 29 },
...   { username: "Creadora contenido 8", email: "creadora8@email.com", age: 26 },
...   { username: "Creadora contenido 9", email: "creadora9@email.com", age: 34 },
...   { username: "Creadora contenido 10", email: "creadora10@email.com", age: 33 }
... ])
```
##2.2 ACTUALIZAR  DATOS
Actualizar publicaciones:

Actualiza todos los valores de los campos de una publicación.

SOLUCIÓN: 
```js
db.posts.updateOne ({title:"Título post 1"},
	{$set:{body:"Contenido actualizado", 
	username:"Creadora actualizada", 
	comment: 
		{username:"comentador actualizado", 
		body:"contenido comentario actualizado"}
}
})
```

Cambiar el valor del campo “body” de una publicación.

SOLUCIÓN: 
```js
db.posts.updateOne ({title:"Título post 1"},
	{$set:{body:"Este es un body muy interesante y actualizado", 
	username:"Creadora actualizada", 
	comment: 
		{username:"comentador actualizado", 
		body:"contenido comentario actualizado"}
}
})
```
Actualizar comentarios:

Todas los nombres son distintos, no puedo llamar a varios de una vez.


Actualiza el comentario de una publicación.

SOLUCIÓN: 
```js
db.posts.updateOne ({title:"Título post 3"},
	{$set:{comment: {username:"USUARIO ACTUALIZADO",body:"CONTENIDO COMENTARIO ACTUALIZADO"}}})
```

Actualizar usuarios:

SOLUCIÓN: Sólo puedo actualizer uno, todos los nombres son diferentes.
```js
db.users.updateOne({username: "Creadora contenido 1"},
{$set:{username: "Mari Pili actualizada", email: "maripi@email.com", age: 37 }})
```
Actualiza todos los valores de los campos de un usuario

SOLUCIÓN: 
```js
db.users.updateOne({username: "Creadora contenido 5"},
{$set:{username: "Maje actualizada", email: "maje@email.com", age: 6 }})
```

Cambiar el email de dos usuarios, es decir, hacer la query dos veces.

SOLUCIÓN: 
```js
db.users.updateOne({username: "Creadora contenido 8"},
{$set:{email: "usuaria7@email.com"}})
```
db.users.updateOne({username: "Creadora contenido 9"},
{$set:{email: "usuaria9@email.com"}})
```
Aumenta en 5 años la edad de un usuario.
```js
db.users.updateOne ({username:"Creadora contenido 4"},
{
$inc: {
	price:5
	}
})
```

##2.3 OBTENER DATOS
Seleccionar todas las publicaciones.

SOLUCIÓN: 
```js
db.posts.find()
```

Selecciona las publicaciones que coincidan con el username indicado.

SOLUCIÓN:
```js
db.users.find({username:"Mari Pili actualizada"})
```

Seleccione todos los usuarios con una edad mayor a 20.

SOLUCIÓN:
```js
db.users.find({age:{$gt:20}})
```
```

Seleccione todos los usuarios con una edad inferior a 23.
```js
db.users.find({age:{$lt:23}})
```

Seleccione todos los usuarios que tengan una edad entre 25 y 30 años.
SOLUCIÓN:
```js
db.users.find({
	$and: [
		{age: {$gte:25}},
		{age: {$lte:30}}
	]
})


({age:{$gte:25},
	$and : [{age:{$lte:30}}]
})
```
Muestra los usuarios de edad menor a mayor y viceversa.

SOLUCIÓN:
```js 
db.users.find().sort({age:-1})
db.users.find().sort({age:1})
```
Seleccione el número total de usuarios.

SOLUCIÓN:
```js
db.users.find().count()
```
Seleccione todas las publicaciones y haz que se muestren con la siguiente estructura: 
Título de la publicación: "title one".

SOLUCIÓN:
```js
db.users.find()
```
Selecciona solo 2 usuarios.
```js
db.users.find().limit(2)
```
Busca por title 2 publicaciones.(haz la misma consulta 2 veces)

SOLUCIÓN:
```js
db.posts.find({title:"Título post 6"})
db.posts.find({title:"Título post 1"})
```

##2.4 BORRAR DATOS

Elimina a todos los usuarios con una edad mayor a 30.

SOLUCIÓN: 
```js 
db.users.deleteMany({age:{$gte:30}})		
```


