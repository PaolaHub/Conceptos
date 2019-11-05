# CORS - Cross Origin Resources Sharing

En la clase pasada intentas hacer el post pero chocamos con un problema del CORS, muchas personas tienden a ver esto como 
un inconveniente un problema serio, y habilitan el CORS en su servidor y se acabo el asunto, que de echo eso es lo que vamos hacer.

Pero entiendan que el CORS es algo bueno, que nosostros tenemos que controlar, normalmente cuando habilitamos el CORS para todos los lugares,
cualquier persona, dese cualquier lugar del mundo, desde cualquier página web, va a poder hacer peticiones put post o que especifiquemos
a nuestro servidor. 

Por lo general es recomendable usar algo para controlar el CORS,existe un middleware **express cors** para trabajar con el cors en express.

https://github.com/expressjs/cors

Yo le recomendaría que para un proyecto ya en producción, para un cliente serio, o algun trabajo en particular, instalen este plugging u
otro en particular, pero generar un middleware como el que ahí aparece. 

 Y ustedes van a poder configurar desde que origenes van a permitir ese tipo de peticiones.
 
        Configuring CORS
        var express = require('express')
        var cors = require('cors')
        var app = express()

        var corsOptions = {
          origin: 'http://example.com',
          optionsSuccessStatus: 200 // some legacy browsers (IE11, various SmartTVs) choke on 204
        }

        app.get('/products/:id', cors(corsOptions), function (req, res, next) {
          res.json({msg: 'This is CORS-enabled for only example.com.'})
        })

        app.listen(80, function () {
          console.log('CORS-enabled web server listening on port 80')
        })
Por ejemplo, si es esto es un local host y nosotros estamos trabajando en una red interna de una empresa, podemos permitir X cantidad de conexiones solo de un dominio en particular o si ustedes tienen un aplicación y la app está montada en un dominio en particular y solo de ahí van a recibir peticiones, les recomendaria que se tomaran la molestia de configurar el cors correctamente.

En nuestro caso, vamos hacerlo de una manera rápida.

https://enable-cors.org/server.html

Seleccionamos el servidor o el código del Backend que nosotros tenemos corriendo ahí.
En nuestro caso es ExpressJS.

Para avitar el CORS, aquí tenemos varios registros, varias formas de hacerlo.

     app.use(function(req, res, next) {
       res.header("Access-Control-Allow-Origin", "YOUR-DOMAIN.TLD"); // update to match the domain you will make the request from
       res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
       next();
     });

     app.get('/', function(req, res, next) {
       // Handle the get for this route
     });

     app.post('/', function(req, res, next) {
      // Handle the post for this route
     });
     
 Este sería el middleware que vamos a copiar, añadiendole una línea más para controlar
 que métodos van a poder estar permitidos. Con el * le estamos diciendo que cualquier lugar va a poder hacer las peticiones.
 
     app.use(function(req, res, next) {
       res.header("Access-Control-Allow-Origin", "*"); // update to match the domain you will make the request from
       res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
       res.header("Access-Control-Allow-Methods", "POST, GET, PUT, DELETE, OPTIONS");
       next();
     });
     

¿Donde lo colocamos?
En nuestro app.js del backend-server




# Por Victor Robles
      // Configurar cabeceras y cors
      app.use((req, res, next) => {
          res.header('Access-Control-Allow-Origin', '*');
          res.header('Access-Control-Allow-Headers', 'Authorization, X-API-KEY, Origin, X-Requested-With, Content-Type, Accept, Access-Control-Allow-Request-Method');
          res.header('Access-Control-Allow-Methods', 'GET, POST, OPTIONS, PUT, DELETE');
          res.header('Allow', 'GET, POST, OPTIONS, PUT, DELETE');
          next();
      });
