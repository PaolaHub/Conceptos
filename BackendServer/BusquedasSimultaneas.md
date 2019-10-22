# Busquedas a diferentes colecciones de forma simultanea (Promise.all)

Para hacer una busqueda en dos o más colecciones diferentes, necesitariamos anidar promesas.
Primero hacemos un Find ... then.. el otro find.. Esto va a tardar mucho, porque vamos a 
tener que esperar a que terminen todas las promesas de una en una y además el código nos queda
muy engorroso.

El ECMAScript6 nos proporciona una nueva function: **Promise.all()**.
Esta función nos permite llamar a diferentes promesas de forma paralela y se define de la siguiente manera:

          var express = require('express');

          var app = express();

          var Hospital = require('../models/hospital');
          var Medico = require('../models/medico');
          var Usuario = require('../models/usuario')

          // Peticion de búsqueda general
          app.get('/todo/:busqueda', (req, res, next) => {

              var busqueda = req.params.busqueda;
              // Expresion regular
              var regex = new RegExp(busqueda, 'i');

              Promise.all([
                      buscarHospitales(busqueda, regex),
                      buscarMedicos(busqueda, regex),
                      buscarUsuarios(busqueda, regex)
                  ])
                  .then(respuestas => {

                      res.status(200).json({
                          ok: true,
                          hospitales: respuestas[0],
                          medicos: respuestas[1],
                          usuarios: respuestas[2]
                      })
                  });
          });


          function buscarHospitales(busqueda, regex) {

              return new Promise((resolver, reject) => {

                  Hospital.find({ nombre: regex })
                      .populate('usuario', 'nombre email')
                      .exec((error, hospitales) => {
                          if (error) {
                              reject('Error al cargar hospitales', error);
                          } else {
                              resolver(hospitales)
                          }
                      });
              });
          }

          function buscarMedicos(busqueda, regex) {

              return new Promise((resolver, reject) => {

                  Medico.find({ nombre: regex })
                      .populate('usuario', 'nombre email')
                      .populate('hospital')
                      .exec((error, medicos) => {
                          if (error) {
                              reject('Error al cargar medicos', error);
                          } else {
                              resolver(medicos)
                          }
                      });
              });
          }

          function buscarUsuarios(busqueda, regex) {

              return new Promise((resolver, reject) => {

                  Usuario.find({}, 'nombre email role')
                      .or([{ 'nombre': regex }, { 'email': regex }])
                      .exec((error, usuarios) => {

                          if (error) {
                              reject('Error al cargar usuarios', err);
                          } else {
                              resolver(usuarios);
                          }
                      });
              });
          }

          module.exports = app;

