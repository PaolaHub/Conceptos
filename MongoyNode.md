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
        
### Ahora vamos a crar las rutas para el usuario:

1. Creamos el archivo **routes/usuario.js**

        var express = require('express');

        var app = express();

        var Usuario = require('../models/usuario');

        // Peticion a la raiz del servicio
        app.get('/', (request, response, next) => {

            Usuario.find({}, (error, usuarios) => {
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



