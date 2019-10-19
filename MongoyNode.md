## Necesario

Para usar estas indicaciones, hay que haber configurador un Backend-Server con Node, Express y Mongo

## Empezamos creando una colección usuarios en Mongo:

1. Levantamos el servidor de Mongo
2. Nos conectamos al puerto
3. Nos vamos a nuestra base de datos y hacemos click derecho en Collectios y creamos usuarios.

                      {
                          "nombre" : "Paola",
                          "email" : "paola@gmail.com",
                          "password" : "123",
                          "img" : null,
                          "role" : "ADMIN_ROLE"
                      }
                      
4. Una vez que se crear, Mongo automáticamente le va añadir una nueva propiedad que es el "id",
para poder liego relacionarlas con otras bases de datos.

## Ahora creamos el modelo en la parte de Node:

1. Creamos una carpeta llamada **Models** (así se la llama standar) en el directorio raiz.
2. Creamos el archivo **usuario.js** y escribimos el siguiente código:

              var mongoose = require('mongoose');

                  var Schema = mongoose.Schema;


                  var usuarioSchema = new Schema({

                      nombre: { type: String, required: [true, 'El nombre es necesario'] },
                      email: { type: String, unique: true, required: [true, 'El email es necesario'] },
                      password: { type: String, required: [true, 'La contraseña es necesaria'] },
                      img: { type: String, required: false },
                      role: { type: String, required: true, default: 'USER_ROLE' }
                  });

              module.exports = mongoose.model('Usuario', usuarioSchema);
              
## Creando las rutas de los servicios de usuario:

### Primero vamos a modularizar las rutas

1. Creamos una carpeta **routes**
2. Vamos a mover las ruta que creamos para realizar la peticion a la raiz del servicio. 
   Creamos un archivo **app.js** en **routes** con el siguiente código:
   
       var express = require('express');
       var app = express();

        // Peticion a la raiz del servicio
        app.get('/', (request, response, next) => {
          response.status(200).json({
              ok: true,
              mensaje: 'Petición realizada correctamente'
          })
       });
       // Para exportar la ruta.
       module.exports = app;
        
3. Ahora tenemos que modificar nuestro archivo app.js del directorio raiz:

        // Importar Rutas. Estamos importando las rutas definidas en el routes/app.js
        var appRoutes = require('./routes/app');

        // Rutas. Estamos definiendo las rutas.
        app.use('/', appRoutes);
        
### Ahora vamos a crear las rutas para el usuarios:

1. Creamos el archivo **routes/usuario.js**

          var express = require('express');

          var app = express();

          var Usuario = require('../models/usuario');

          // Peticion a la raiz del servicio
          app.get('/', (request, response, next) => {

              Usuario.find({}, 'nombre email img role')
                  .exec(
                      (error, usuarios) => {
                          if (error) {
                              return response.status(500).json({
                                  ok: false,
                                  mensaje: 'Error cargando usuarios',
                                  errors: error
                              })
                          }
                          response.status(200).json({
                              ok: true,
                              usuarios: usuarios
                          });
                      });
          });

          module.exports = app;
     
2. Modificamos el archivo **app.js**

        // Importar Rutas
        var appRoutes = require('./routes/app');
        var usuarioRoutes = require('./routes/usuario');

        // Rutas
        app.use('/usuario', usuarioRoutes);
        app.use('/', appRoutes);
        
3. Si vamos a Postman y probamos las dos rutas haciendo un get:

**http://localhost:3000/**

**http://localhost:3000/usuario**

Nos deberían de salir los mensajes correctos y los usuarios de la base de datos de Mongo.

## Creando un usuario (POST)

Para poder pasar comodamente los datos de entradda a una peqtición POST,
tenemos un paquete en GitHub que se llama **body-parser**.

### Descargamos el BODY-Parser

**npm install body-parser --save**

### Ahora vamos a configurarlo en el **app.js**

      var bodyParser = require('body-parser');

      // Body Parser
      // parse application/x-www-form-urlencoded
      app.use(bodyParser.urlencoded({ extended: false }));
      app.use(bodyParser.json());
      
## Ahora vamos a crear la petición POST en routes/usuario.js

        app.post('/', (req, response) => {
        
          var body = req.body;

          var usuario = new Usuario({
              nombre: body.nombre,
              email: body.email,
              password: body.password,
              img: body.img,
              role: body.role
          });

          usuario.save((error, usuarioGuardado) => {

              if (error) {
                  return response.status(500).json({
                      ok: false,
                      mensaje: 'Error al crear usuarios',
                      errors: error
                  });
              }
              response.status(201).json({
                  ok: true,
                  usuario: usuarioGuardado
              });

          });
    });

    module.exports = app;
    
### Para probarlo, nos vamos al POSTMAN

POST => **http://localhost:3000/usuario**
En el **Body** usamos x-www-form-urlencoded
He introducimos los datos que queremos.
Aquí podemos ver que si no introducimos los valores como en el esquema definido,
desde Mongoo nos van a salir los mensajes de error.

### Validaciones

Mongoose tiene un plugin para hacer que los mensaje de error por "Unique" se vean mejor

**npm install mongoose-unique-validator --save**

Ese plugin lo añadimos al **models/usuarios.js**

    var mongoose = require('mongoose');
    var uniqueValidator = require('mongoose-unique-validator');

    var Schema = mongoose.Schema;

    var rolesValidos = {
        values: ['ADMIN_ROLE', 'USER_ROLE'],
        message: '{VALUE} no es un rol permitido'
    };

    // Definición del esquema
    var usuarioSchema = new Schema({

        nombre: { type: String, required: [true, 'El nombre es necesario'] },
        email: { type: String, unique: true, required: [true, 'El email es necesario'] },
        password: { type: String, required: [true, 'La contraseña es necesaria'] },
        img: { type: String, required: false },
        role: { type: String, required: true, default: 'USER_ROLE', enum: rolesValidos }
    });

    // Aquí le decimos al esquema de usuarios que ese esquema tiene el uniqueValidator y le podemos definor el mensaje.
    usuarioSchema.plugin(uniqueValidator, { message: '{PATH} debe de ser único' });

    // Para poder usarlo fuera hay que exportarlo.
    module.exports = mongoose.model('Usuario', usuarioSchema);
    
En este mismo ejemplo, se ha definidos unos parámetros para el campo "ROL": 

    var rolesValidos = {
        values: ['ADMIN_ROLE', 'USER_ROLE'],
        message: '{VALUE} no es un rol permitido'
    };
    
para hacerselo saber:

    role: { type: String, required: true, default: 'USER_ROLE', enum: rolesValidos }
    
    
## Para encriptar una contraseña

Para encriptar una contraseña hay un pluging bastante conocido en GitHub que es el bscrypt.js
Esta es una encriptación de una sola vía.

Lo instalamos **npm install bcryptjs --save** (--save porque será una dependencia de nuestro projecto).

La añadimos en **routes/usuario.js**

y la usamos al crear al usuario:

    var usuario = new Usuario({
        nombre: body.nombre,
        email: body.email,
        password: bcrypt.hashSync(body.password, 10),
        img: body.img,
        role: body.role
    });

Si creamos un nuevo usuario con el Postman, veremos que ahora la contraseña está encriptada.

## Actualizar un usuario (PUT)

Vamos a crear otra petición en el **routes/usario.js**.
Aquí vamos a cambiar la ruta con **'/:id** porque necesitamos el id
del elemento que vamos a modificar.

1. Primero vamos a coger de los **params** el id que se encuentra en el url.
2. Segundo vamos a coger los elementos del **body** con los que queremos actualizar.
3. Vamos a buscar en nuestra collection **Usuarios** si realmente existe ese "id".
4. Definimos los erroes, si no lo encuentra, el objecto **usuario** vendría vacio,
así que si se produce algún **error**, será por la conexión o a saber, es por eso
que lo definimos con el error 500.
(Tenemos un pdf con todos los errores y deberíamos definirlo bien, porque
esto nos va ayudar mucho del lado de Angular)
5. Luego vamos a actulizar el **usuario** de la respuesta del **findById**
por el **request.body** y lo salvamos.
6. La petición nos devolverá el objeto guardado si todo ha salido correctamenta.
Para no ver la contraseña del usuario. La modificamos, pero esta modificación solo
se hace para devolver el objecto dentro del callback. Eso quiere decir, que no estamos
guardando ese valor en la base de datos.



      app.put('/:id', (request, response, next) => {

          var id = request.params.id;
          var body = request.body;

          Usuario.findById(id, (error, usuario) => {

              if (error) {
                  return response.status(500).json({
                      ok: false,
                      mensaje: 'Error al buscar usuario',
                      errors: error
                  });
              }

              if (!usuario) {
                  return response.status(400).json({
                      ok: false,
                      mensaje: 'El usuario con el id' + id + ' no existe',
                      errors: { message: 'No existe un usuario con ese ID' }
                  });
              }

              usuario.nombre = body.nombre;
              usuario.email = body.email;
              usuario.role = body.role;

              usuario.save((error, usuarioGuardado) => {
                  if (error) {
                      return response.status(400).json({
                          ok: false,
                          mensaje: 'Error al actualizar usuarios',
                          errors: error
                      });
                  }

                  // Esta es otra manera de modificar los datos que se le van a pasar.
                  // OJO que no estamos guardando la carita feliz, porque la estamos
                  // definiendo en el callback. La funcion save ya se hizo.
                  usuarioGuardado.password = ':)';

                  response.status(200).json({
                      ok: true,
                      usuario: usuarioGuardado
                  });
              });
          });
      });




    











