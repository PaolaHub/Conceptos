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
              
## Creando las rutas de los servicios de usuario (GET)

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

Para poder pasar comodamente los datos de entradda a una petición POST,
tenemos un paquete en GitHub que se llama **body-parser**.

### Descargamos el BODY-Parser

**npm install body-parser --save**

### Ahora vamos a configurarlo en el **app.js**

      var bodyParser = require('body-parser');

      // Body Parser
      // parse application/x-www-form-urlencoded
      app.use(bodyParser.urlencoded({ extended: false }));
      app.use(bodyParser.json());
      
### Ahora vamos a crear la petición POST en routes/usuario.js

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
    
    
## Enncriptar una contraseña

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
3. Vamos a buscar en nuestro modelo **Usuarios** si realmente existe ese "id".
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
      
## Borrar un usuario (DELETE)

Nos vamos nuevamente a las rutas **routes/usuario.js**, y creamos la petición de delete:
*NOTA: El nombre que definamos en la ruta (**este_id**) es el mismo que tenemos que usar cuando llamamos a los params.*

    app.delete('/:este_id', (request, response, next) => {
    
    var id = request.params.este_id;

    Usuario.findByIdAndDelete(id, (error, usuarioBorrado) => {

        if (error) {
            return response.status(500).json({
                ok: false,
                mensaje: 'Error al borrar usuario',
                errors: error
            });
        }

        if (!usuarioBorrado) {
            return response.status(400).json({
                ok: false,
                mensaje: 'No existe un usuario con ese id',
                errors: { message: 'No existe un usuario con ese id' }
            });
        }

        response.status(200).json({
            ok: true,
            usuario: usuarioBorrado
        });
    });
    });

## Autenticación y Login (POST)

Vamos a crear otras routes para la autentificación
 1. Creamos un nuevo archivo **routes/login.js**
 2. Importamos lo necesario:
  * El express porque vamos hacer peticiones.
  * Bcrypt porque vamos a tener que comparar las encriptaciones.
  * Vamos a levantar el servicio Express.
  * Vamos a crearnos nuestro modelo, porque vamos a tener que ver si existe el usuario.
  * Para poder usarlo fuera del archivo, vamos a exportarlo.
 
        var express = require('express');
        var bcrypt = require('bcryptjs');


        var app = express();

        var Usuario = require('../models/usuario');

        module.exports = app;
        
 3. Ahora vamos a usar nuestro archivo **app.js**
  * Importamos el archivo de routes (**var loginRoutes = require('./routes/login');**)
  * Creamos el middleware **use** (**app.use('/login', loginRoutes);**)
  
  4. Ahora vamos a crear nuestra petición POST.
    
    app.post('/', (request, response, next) => {
    
      var body = request.body;

      Usuario.findOne({ email: body.email }, (error, usuarioDB) => {

          if (error) {
              return response.status(500).json({
                  ok: false,
                  mensaje: 'Error al buscar usuarios',
                  errors: error
              });
          }

          if (!usuarioDB) {
              return response.status(400).json({
                  ok: false,
                  mensaje: 'Credenciales incorrectas - email',
                  errors: error
              });
          }

          if (!bcrypt.compareSync(body.password, usuarioDB.password)) {
              return response.status(400).json({
                  ok: false,
                  mensaje: 'Credenciales incorrectas - password',
                  errors: error
              });
          }

          // Crear un token!!!
          usuarioDB.password = ':)';
          // 1. PAYLOAD. Tenemos que poner la data que queremos colocar en el token, se conoce como el payload
          // 2. SEED. Algo que nos ayude a hacer unico a nuestro token.
          // 3. Fecha de expiración en segundos. 4 horas
          var token = jwt.sign({ usuario: usuarioDB }, 'este-es-un-seed-dificil', { expiresIn: 14400 })

          response.status(200).json({
              ok: true,
              usuario: usuarioDB,
              token: token,
              id: usuarioDB._id
          });
      });
      
  5. Crear Token
  Para crear el token que ves en el ejemplo de arriba, hemos instalado un paquete
  
  **https://github.com/auth0/node-jsonwebtoken**
  
  Lo instalamos:
  
  **npm install jsonwebtoken --save**
  
 Si vamos al POSTMAN y enviamos la petición, nos saldra el token.
 Con este token vamos a la página
 
 **https://jwt.io/**
 
 ahí pegamos el token y también el SEED. y nos autentificará el token.
 
 
## Limitar las acciones solo si está autenticado.

Vamos a hacer que el Actualizar, Crear y Borrar, solo lo puedan hacer usuarios autenticados con un token.
Para ello:

1. Vamos a crear una nueva carpeta en el directorio raiz **middlewares**
NOTA: Un middleware es algo que queremos que se ejecute.
2. Creamos el archivo **autenticacion.ts** con el siguiente código.

        var jwt = require('jsonwebtoken');

        var SEED = require('../config/config').SEED;

        // ==============================
        //  Verificar token
        // ==============================
        exports.verificaToken = function(request, response, next) {

            var token = request.query.token;

            jwt.verify(token, SEED, (error, decoded) => {

                if (error) {
                    return response.status(401).json({
                        ok: false,
                        mensaje: 'Token incorrecto',
                        errors: error
                    })
                }

                request.usuario = decoded.usuario;

                next();
                // return response.status(200).json({
                //     ok: true,
                //     decoded: decoded
                // })
            });
          }


3. Lo que hacemos es crear una funcion la cual vamos a tener que exportar.
Esa funcion tiene un **request, responde y next**.
4. Esa funcion necesita el token que lo cojemos de la url, y va llamar a la libreria de **jwt** para verificar el token,
con el **SEED**.
5. El **decoded** del callback de jwt.verify, contiene los datos que se usaron para la encriptación.
Es por eso que lo guardamos en el variable request, para que todas las funciones que 
pasen por esta autenticacion, tengan quien hizo la acción.
6. Despues llamamos a la función **next()**, que va permitir ir corriendo las demás peticiones.

7. Para usarlo:

        app.put('/:id', mdAutenticacion.verificaToken, (request, response, next) => {
        
    También puede mandarse más middleware en un arreglo [mdAutenticacion.verificaToken, mdAutenticacion1.verificaToken1]
    Cuando mandemos la respuesta buena, le mandamos **usuarioToken: req.usuario**

        response.status(201).json({
            ok: true,
            usuario: usuarioGuardado,
            usuarioToken: req.usuario
        });



## Relacionar Tablas

Se usa él : **type: Schema.Types.ObjectId, ref: 'Usuario'**

    var mongoose = require('mongoose');

    var Schema = mongoose.Schema;
    var medicoSchema = new Schema({
        nombre: { type: String, required: [true, 'El nombre	es necesario'] },
        img: { type: String, required: false },
        usuario: { type: Schema.Types.ObjectId, ref: 'Usuario', required: true },
        hospital: {
            type: Schema.Types.ObjectId,
            ref: 'Hospital',
            required: [true, 'El id	hospital es un campo obligatorio ']
        }
    });

    module.exports = mongoose.model('Medico', medicoSchema);

### Si se quiere relacionar más de un hospital a un médico:


        hospital: [{
            type: Schema.Types.ObjectId,
            ref: 'Hospital',
            required: [true, 'El id	hospital es un campo obligatorio ']
        }]
        
### En POST Y PUT
1. POST:

        var medico = new Medico({
            nombre: body.nombre,
            usuario: req.usuario._id,
            hospital: body.hospital
        });
2. PUT:

         medico.nombre = body.nombre;
         medico.usuario = req.usuario._id;
         medico.hospital = body.hospital;

### Schema
**{	collection:	‘hospitales’ }** esto	simplemente	es	para	
evitar	que	Mongoose	coloque	el	nombre	a	la	colección como	hospitals.

    var hospitalSchema = new Schema({
        nombre: { type: String, required: [true, 'El	nombre	es	necesario'] },
        img: { type: String, required: false },
        usuario: { type: Schema.Types.ObjectId, ref: 'Usuario' }
    }, { collection: 'hospitales' });
    
### POPULATE en los GET (Obtener información de otras tablas)

Si un esquema contiene alguna relación por id con otra table,
podemos hacer que nos aparezca a parte del id, todo su contenido usando la función populate.
Sabemos que Medico contiene dos parámetros en su esquema, que son dos referencias a que **USUARIO** creo el medico
y en que **HOPSITAL** se encuentra ese médico.
Es por ello, que usamos dos populate.

    // Petición GET
    app.get('/', (req, res, next) => {
    Medico.find()
        .populate('usuario', 'nombre email')
        .populate('hospital')
        .exec((error, medicos) => {
            if (error) {
                return res.status(500).json({
                    ok: false,
                    mensaje: 'Error al cargar los medicos',
                    errors: error
                });
            }

            res.status(200).json({
                ok: true,
                medicos: medicos
            });
        });
        });
