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
