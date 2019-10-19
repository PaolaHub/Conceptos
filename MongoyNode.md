## Empezamos creando una colección usuarios en Mongo:

1. Levantamos el servidor de Mongo
2. Nos conectamos al puerto
3. Nos vamos a nuestra base de datos y hacemos click derecho en Collectios y creamos usuarios.

                      {
                          "nombre" : "Fernando",
                          "email" : "fernando@gmail.com",
                          "password" : "123",
                          "img" : null,
                          "role" : "ADMIN_ROLE"
                      }
                      
4. Una vez que se crear, Mongo automáticamente le va añadir una nueva propiedad que es el "id",
para poder liego relacionarlas con otras bases de datos.

## Ahora creamos el modelo en la parte de Node:

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
