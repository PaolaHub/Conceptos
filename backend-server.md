# Backend-server desde 0

#### Creando el proyecto NODE e instalando EXPRESS

1. Creamos una carpeta y nos dirigimos a ella en la termina.
2. Ejecutamos el commando **npm init** para iniciar node. **NODE es simplemente JavaScript corriendo del lado del servidor**.
3. Luego vamos a descargarnos el servidor **expressjs.com** porque es muy fácil hacer peticiones o servicios REST en el lado de NODE.
  * Para descargarlo, ejecutamos el comando **npm install express --save** ( el --save es para indicar que esa librería es necesaria para que funcione nuestro servidor en nuestro proyecto de NODE).
  Si nos fijamos instala en la carpeta los módulos de NODE y todo lo necesario para que funcione Express.
  
#### Inicializando el servidor

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


