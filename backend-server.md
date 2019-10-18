# Backend-server desde 0

### Creando el proyecto NODE e instalando EXPRESS

1. Creamos una carpeta y nos dirigimos a ella en la termina.
2. Ejecutamos el commando **npm init** para iniciar node. **NODE es simplemente JavaScript corriendo del lado del servidor**.
3. Luego vamos a descargarnos el servidor **expressjs.com** porque es muy fácil hacer peticiones o servicios REST en el lado de NODE.
  * Para descargarlo, ejecutamos el comando **npm install express --save** ( el --save es para indicar que esa librería es necesaria para que funcione nuestro servidor en nuestro proyecto de NODE).
  Si nos fijamos instala en la carpeta los módulos de NODE y todo lo necesario para que funcione Express.
  
### Inicializando el servidor

1. Creamos un archivo **app.js** en el directorio raiz. Ese archivo es el punto de entrada de nuestra aplicación
y va a contener todo el código JavaScript que va a inicializar nuestro servidor Express, entre otras cosas
como la base de datos, autentificaciones, rutas, etc...

2. Escribimos el siguiente código, para inicializar el servidor Express.

            // Requires
            var express = require('express'); // Cargamos la librería de Espress


            // Inicializar variables
            var app = express(); // Vamos a crear la aplicación de Espress. Así ya estamos definiendo el servidor Espress.

            // Escuchar peticiones. Queremos que escuche el puerto 3000 y nos muestre un mensaje para saber si lo logro levantar.
            app.listen(3000, () => {
                console.log("Express server puerto 3000 online");
            });
            
3. Para ver si funciona, nos vamos a la terminal y ejecutamos el comando **node app**.
4. Ir al navegador y navegar a localhost:3000. Vemos que nos aparece un Cannot GET, y eso es por que no existe ninguna ruta que
coincida con esto, pero el servidor ya está corriendo.

### Para cambiar los colores del texto en la consola

console.log('Express server puerto 3000: **\x1b[5m%s\x1b[0m**', 'online');

       Colores para la consola
       
       Reset = "\x1b[0m"

       Bright = "\x1b[1m"

       Dim = "\x1b[2m"

       Underscore = "\x1b[4m"

       Blink = "\x1b[5m"

       Reverse = "\x1b[7m"

       Hidden = "\x1b[8m"

       FgBlack = "\x1b[30m"

       FgRed = "\x1b[31m"

       FgGreen = "\x1b[32m"

       FgYellow = "\x1b[33m"

       FgBlue = "\x1b[34m"

       FgMagenta = "\x1b[35m"

       FgCyan = "\x1b[36m"

       FgWhite = "\x1b[37m"

       BgBlack = "\x1b[40m"

       BgRed = "\x1b[41m"

       BgGreen = "\x1b[42m"

       BgYellow = "\x1b[43m"

       BgBlue = "\x1b[44m"

       BgMagenta = "\x1b[45m"

       BgCyan = "\x1b[46m"

       BgWhite = "\x1b[47m"


### Crear la primera ruta

Creamos la primera ruta en el app.js

    app.get('/', (req, res, next) => {
        res.status(200).json({
            ok: true,
            mensaje: 'Petición realizada correctamente'
        })
    });
    
Para ver si está funcionando, hay que bajar el servidor en la terminal y volver a levantarlo.
Ahora vemos que nos devuelve un JSON.

##### Vamos a probar con Postman
Mientras el servidor está corriendo, vamos a introducir **localhost:3000** como petición GET, en el 
postman. De esta manera verificamos que todas las peticiones se están haciendo correctamente.

### NODEMON - Monitoriza el backend
Para no tener que estar bajando y subiendo el servidor a cada cambio, existe una librería NODEMON.
Vamos a instalarla:
De forma global: **npm install -g nodemon** (va a pedir ser el admintrador)
Solo para el proyecto de desarrollo: **npm install --save-dev nodemon**

La instalamos de la segunda forma.

####¿Como la hechamos a correr?

Vamos en los scripts del package.json escribimos el siguiente código:

    "scripts": {
      "start": "nodemon app.js"
    },
    
Esto hace que se llame al nodemon definiendole el archivo de inicialización del servidor, cuando escribimos "start".
Ahora vamos a la terminal y en vez de escrbir **node app**, escribimos **npm start** (que sería lo mismo que escribir nodemon app.js) 
Y vemos como se está monitorizando. Para probarlo solo tenemos que hacer algún cambio en el código.

