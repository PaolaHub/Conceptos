# Vamos a subir una imagen

Para ello vamos a descargarnos una librería:

**express-fileupload** de https://github.com/richardgirges/express-fileupload

Creamos una nueva ruta **upload.js** y la importamos y definimos en el **app.js**, como siempre

En el archivo **upload.js** escribimos el siguiente código:

          var express = require('express');
          // Importamos la librería
          const fileUpload = require('express-fileupload');

          var app = express();

          // default options - Middleware
          app.use(fileUpload());

          // Es una petición put porque lo que queremos hacer es modificar la "img"
          // de las coleccion usuario, hospitales y medicos.
          
          // En la ruta tenemos que indicarle, a que colección va la imagene
          // y también el id de la instancia.
          app.put('/:tipo/:id', (req, res, next) => {

              var tipo = req.params.tipo;
              var id = req.params.id;

              // Tipo de colección
              var tipoValidos = ['hospitales', 'medicos', 'usuarios'];
              
              // Validando el tipo que llega de la ruta
              if (tipoValidos.indexOf(tipo) < 0) {
                  return res.status(400).json({
                      ok: false,
                      mensaje: 'Tipo de colección no válida',
                      errors: { message: 'Tipo de colección no válida' }
                  });
              }

              // Validamos si no se ha seleccionado ningún archivo.
              if (!req.files) {
                  return res.status(400).json({
                      ok: false,
                      mensaje: 'No selecciono nada',
                      errors: { message: 'Debe de seleccionar una imagen' }
                  });
              }

              // Obtener nombre del archivo
              // ".imagen" es la variable que definimos en el postman cuando le pasamos el archivo
              // Este archivo se pasa por el "body" como "form-data". Se selecciona "File"
              // y seleccionamos con el browser un archivo para hacer pruebas.
              var archivo = req.files.imagen;
              
              // Vamos a sacar la extension para luego comprobar si es realmente una imagen lo 
              // que hemos subido como archivo.
              var nombreCortado = archivo.name.split('.');
              var extensionArchivo = nombreCortado[nombreCortado.length - 1];

              // Sólo estas extensiones aceptamos
              var extensionesValidas = ['png', 'jpg', 'gif', 'jpeg'];

              // Validación del tipo del archivo subido.
              if (extensionesValidas.indexOf(extensionArchivo) < 0) {
                  return res.status(400).json({
                      ok: false,
                      mensaje: 'Extensión no válida',
                      errors: { message: 'Las extensiones válidas son: ' + extensionesValidas.join(', ') }
                  });
              }

              // Nombre de archivo personalizado 
              // Al archivo que guardamos en el backend, le cambiamos el nombre para que no cree conflictos.
              var nombreArchivo = `${ id }-${ new Date().getMilliseconds() }.${extensionArchivo}`;

              // Mover el archivo del temporal al path (a nuestro backendserver, para eso creamos una carpeta en el directorio
              // raiz "uploads" y dentro tres carpetas más "medicos", "hospitales" y "usuarios".)
              var path = `./uploads/${tipo}/${nombreArchivo}`;
              archivo.mv(path, (error) => {
                  if (error) {
                      return res.status(500).json({
                          ok: false,
                          mensaje: 'Error al mover archivo',
                          errors: error
                      });
                  }
              });


              res.status(200).json({
                  ok: true,
                  mensaje: 'Archivo movido',
                  extensionArchivo: extensionArchivo
              })
          });

          module.exports = app;
          
### Asignar la foto a un usuario, medico u hospital y eliminar la fotografía anterior

Anteriormente hemos visto como subir una foto, ahora tenemos que asignar la foto y si actualizamos por otra,
borrar la anterior para que no se nos llene de archivos.var express = require('express');

                    // Librería externa, hay que descargarla con npm.
                    const fileUpload = require('express-fileupload');

                    // Esto no hay que descargarselo, viene ya en node.
                    // Solo escribimos y lo usamos
                    var fs = require('fs');

                    var app = express();

                    // default options
                    app.use(fileUpload());

                    var Usuario = require('../models/usuario');
                    var Medico = require('../models/medico');
                    var Hospital = require('../models/hospital');

                    // Peticion a la raiz del servicio
                    app.put('/:tipo/:id', (req, res, next) => {

                        var tipo = req.params.tipo;
                        var id = req.params.id;

                        // Tipo de colección
                        var tipoValidos = ['hospitales', 'medicos', 'usuarios'];
                        if (tipoValidos.indexOf(tipo) < 0) {
                            return res.status(400).json({
                                ok: false,
                                mensaje: 'Tipo de colección no válida',
                                errors: { message: 'Tipo de colección no válida' }
                            });
                        }

                        if (!req.files) {
                            return res.status(400).json({
                                ok: false,
                                mensaje: 'No selecciono nada',
                                errors: { message: 'Debe de seleccionar una imagen' }
                            });
                        }

                        // Obtener nombre del archivo
                        var archivo = req.files.imagen;
                        var nombreCortado = archivo.name.split('.');
                        var extensionArchivo = nombreCortado[nombreCortado.length - 1];

                        // Sólo estas extensiones aceptamos
                        var extensionesValidas = ['png', 'jpg', 'gif', 'jpeg'];

                        if (extensionesValidas.indexOf(extensionArchivo) < 0) {
                            return res.status(400).json({
                                ok: false,
                                mensaje: 'Extensión no válida',
                                errors: { message: 'Las extensiones válidas son: ' + extensionesValidas.join(', ') }
                            });
                        }

                        // Nombre de archivo personalizado 
                        var nombreArchivo = `${ id }-${ new Date().getMilliseconds() }.${extensionArchivo}`;

                        // Mover el archivo del temporal al path
                        var path = `./uploads/${tipo}/${nombreArchivo}`;

                        archivo.mv(path, (error) => {
                            if (error) {
                                return res.status(500).json({
                                    ok: false,
                                    mensaje: 'Error al mover archivo',
                                    errors: error
                                });
                            }
                        });

                        subirPorTipo(tipo, id, nombreArchivo, res);

                        // Comentamos esta respuesta porque no queremos que salga por aquí,
                        // si no por la funcion subirPorTipo.
                        // res.status(200).json({
                        //     ok: true,
                        //     mensaje: 'Archivo movido',
                        //     extensionArchivo: extensionArchivo
                        // })
                    });

                    //res : Porque yo quiero sacar la respuesta en formato json desde esta funcion
                    function subirPorTipo(tipo, id, nombreArchivo, res) {

                        if (tipo === 'usuarios') {

                            Usuario.findById(id, (error, usuario) => {

                                if (error) {
                                    return res.status(500).json({
                                        ok: false,
                                        mensaje: 'Error al buscar usuario',
                                        errors: error
                                    });
                                }

                                if (!usuario) {
                                    return res.status(400).json({
                                        ok: false,
                                        mensaje: 'El usuario con el id' + id + ' no existe',
                                        errors: { message: 'No existe un usuario con ese ID' }
                                    });
                                }

                                // Buscamos el path viejo de la imagen.
                                var pathViejo = './uploads/usuarios/' + usuario.img;

                                // Validamos que existe el archivo y lo borramos
                                if (fs.existsSync(pathViejo)) {
                                    fs.unlink(pathViejo);
                                }

                                usuario.img = nombreArchivo;

                                usuario.save((error, usuarioActualizado) => {

                                    if (error) {
                                        return res.status(500).json({
                                            ok: false,
                                            mensaje: 'La imagen de usuario no se ha podido guardar en el registro',
                                            errors: error
                                        });
                                    }

                                    usuarioActualizado.password = ':)';

                                    return res.status(200).json({
                                        ok: true,
                                        mensaje: 'Imagen de usuario actualizada',
                                        usuario: usuarioActualizado
                                    })
                                });
                            });

                        }
                        if (tipo === 'medicos') {

                            Medico.findById(id, (error, medico) => {

                                if (error) {
                                    return res.status(500).json({
                                        ok: false,
                                        mensaje: 'Error al buscar medico',
                                        errors: error
                                    });
                                }

                                if (!medico) {
                                    return res.status(400).json({
                                        ok: false,
                                        mensaje: 'El medico con el id' + id + ' no existe',
                                        errors: { message: 'No existe un medico con ese ID' }
                                    });
                                }

                                // Buscamos el path viejo de la imagen.
                                var pathViejo = './uploads/medicos/' + medico.img;

                                // Validamos que existe el archivo y lo borramos
                                if (fs.existsSync(pathViejo)) {
                                    fs.unlink(pathViejo);
                                }

                                medico.img = nombreArchivo;

                                medico.save((error, medicoActualizado) => {
                                    if (error) {
                                        return res.status(500).json({
                                            ok: false,
                                            mensaje: 'La imagen del medico no se ha podido guardar en el registro',
                                            errors: error
                                        });
                                    }

                                    return res.status(200).json({
                                        ok: true,
                                        mensaje: 'Imagen del medico actualizada',
                                        medico: medicoActualizado
                                    })
                                });
                            });
                        }
                        if (tipo === 'hospitales') {

                            Hospital.findById(id, (error, hospital) => {

                                if (error) {
                                    return res.status(500).json({
                                        ok: false,
                                        mensaje: 'Error al buscar el hospital',
                                        errors: error
                                    });
                                }

                                if (!hospital) {
                                    return res.status(400).json({
                                        ok: false,
                                        mensaje: 'El hospital con el id' + id + ' no existe',
                                        errors: { message: 'No existe un hospital con ese ID' }
                                    });
                                }

                                // Buscamos el path viejo de la imagen.
                                var pathViejo = './uploads/hospitales/' + hospital.img;

                                // Validamos que existe el archivo y lo borramos
                                if (fs.existsSync(pathViejo)) {
                                    fs.unlink(pathViejo);
                                }

                                hospital.img = nombreArchivo;

                                hospital.save((error, hospitalActualizado) => {
                                    if (error) {
                                        return res.status(500).json({
                                            ok: false,
                                            mensaje: 'La imagen del hospital no se ha podido guardar en el registro',
                                            errors: error
                                        });
                                    }

                                    return res.status(200).json({
                                        ok: true,
                                        mensaje: 'Imagen del hospital actualizada',
                                        hospital: hospitalActualizado
                                    })
                                });
                            });
                        }
                    }

                    module.exports = app;


# Desplegar imagenes: FileSystem

Hay un pluggin en GitHub => https://github.com/expressjs/serve-index
que podemos instalarlo y con muy poco código nos crea una ruta
donde se pueden ver las carpetas creadas en el uploads.

Una vez descargado el paquete con **npm install serve-index --save**.
Definimos la configuracion en nuestro **app.js**

          // Server index config ()
          var serveIndex = require('serve-index');
          app.use(express.static(__dirname + '/'));
          app.use('/uploads', serveIndex(__dirname + '/uploads'));
 
Si nos vamos ahora al navegador y escribimos => **localhost:3000/uploads**
Nos aparecen las carpetas y dentro de ellas las fotos que hemos subido.
Nos crea un sistema de archivos, usando ese plugging.

####¿Cuál es el problema con esta librería?
Que cualquiera que se sepa la ruta va poder tener accedo a las imagenes.
Por ello esta solución no es la más apropiada en nuestro caso.

# Crear una ruta para obtener las imagenes

Cremos una nueva ruta en **routes/imagenes.js**

          var express = require('express');

          var app = express();
          
          app.get('/', (request, response, next) => {
              response.status(200).json({
                  ok: true,
                  mensaje: 'Petición realizada correctamente'
              })
          });

          module.exports = app;
          
La importamos y definimos en el **app.js**

          var imagenesRoutes = require('./routes/imagenes');
          app.use('/img', imagenesRoutes);
          
Nuestra ruta en el postman será:

**localhost:3000/img/usuarios/imagensubida.jpg**

1. Necesitamos saber el nombre de la carpeta donde buscar (usuarios, medicos, hospitales del uploads).
2. Necesitamos saber el nombre de la imagen también.
3. Nuestro código quedará de esta manera:

          var express = require('express');

          var app = express();

          // Este path ya viene con Node, no hay que instalar nada.
          const path = require('path');
          const fs = require('fs');


          app.get('/:tipo/:img', (req, res, next) => {

              // El tipo tiene que ser igual al nombre de las carpetas que están en el uploads.
              var tipo = req.params.tipo;
              var img = req.params.img;

              // Definimos la ruta donde está la imagen:
              var pathImagen = path.resolve(__dirname, `../uploads/${ tipo }/${img}`);

              // Validamos que la ruta existe y la enviamos en el res, si no, enviamos una imagen preparada.
              if (fs.existsSync(pathImagen)) {
                  res.sendFile(pathImagen);
              } else {
                  var pathNoImagen = pathImagen = path.resolve(__dirname, '../assets/no-img.jpg');
                  res.sendFile(pathImagen);
              }
          });

          module.exports = app;





