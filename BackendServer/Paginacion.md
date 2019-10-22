# Paginación de una petición (SKIP & LIMIT)

Podemos limitar el número de registros que enviamos desde Mongo.
Para ello se usan dos funciones de Mongoose **LIMIT Y SKIP**.

Tenemos el siguiente código donde definimos una petición GET:

          app.get('/', (req, res, next) => {

              var desde = req.query.desde || 0;
              desde = Number(desde);

              // Esta es una manera de devolver los parámetros que queramos y no todos.
              Usuario.find({}, 'nombre email img role')
                  .skip(desde)
                  .limit(5)
                  .exec(
                      (error, usuarios) => {
                          if (error) {
                              return res.status(500).json({
                                  ok: false,
                                  mensaje: 'Error cargando usuarios',
                                  errors: error
                              })
                          }

                          Usuario.count({}, (error, conteo) => {
                              res.status(200).json({
                                  ok: true,
                                  usuarios: usuarios,
                                  usuarioToken: req.usuario,
                                  total: conteo
                              })
                          });
                      });
          });
          
1. LIMIT 

Hacemos que limitemos el número de registros a 5.
Esto va hacer que nos saque los 5 primeros.
**.limit(5)**
¿Pero como vamos sacando el resto? Hay es donde entra el skip.

2. SKIP

Con el skip vamos a decir cuantos registros queremos saltarnos.
El skip suponemos que nos entra como un valor opcional en la query, sino es 0.
Por eso definimos el siguiente código:

              var desde = req.query.desde || 0;
              desde = Number(desde);
              
Nos tenemos que asegurar que el número que nos llega es un número
y no otra cosa, si la persona ingresa una palabra, el código va a petar.

Una vez definimos el **.skip(desde)**

3. COUNT

Para saber el número de registros que hay,
usamos otra funcion de Mongoose **.count()**, como en el ejemplo.


