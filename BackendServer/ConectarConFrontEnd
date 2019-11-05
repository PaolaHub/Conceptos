
# Vamos a conectar el Backend con el Frontend

Lo primero que tenemos que hacer es tener abierto:

1. Mongo (mongod.exe)
2. Backend-Server (npm start)
3. Frontend (ng serve -o)
4. Visual Studio con la carpeta del frontend.

## Creando un modelo de usuario en el Frontend

Lo primero que haces es observar a los usuario en la base de datos.
Vemos que los usuarios tienen sus propiedades que definimos en el backend-Server.

Para poder comunicarnos entonces de manera fácil, vamos a crearnos en el Frontend
también un modelo de datos de usuario, para que cada vez que recibamos o enviemos
información la hagamos siguiendo el mismo modelo.

Entonces, en el Frontend, en **src/app** creamos una nueva carpeta **models**.
Dentro creamos el archivo **usuario.model.ts** y definimos nuestro modelo en typescript:

            export class Usuario {

                constructor(
                    public nombre: string,
                    public email: string,
                    public password: string,
                    public img?: string,
                    public role?: string,
                    public google?: boolean,
                    // tslint:disable-next-line: variable-name
                    public _id?: string
                ) {}

            }
                
 ## Creando usuarios
 
Una vez creado nuestro modelo, vamos a crear los servicios.
En este ejemplo vamos a crear el servicio usuarios para crear un nuevo usuario en el registro, o hacer un login.
**ng g s services/usuario/usuario** => **app/services/usuario/usuario.service.ts**.

Aquí es donde nos conectamos con el Backend-Serve a través de peticiones HTTP.
Es por eso que necesitamos importar el **HttpClient**, pero para hacer esta importación, tenemos que importar 
su modulo en el modulo donde sea necesario **HttpClientModule**.

Vamos a ir describiendo las cosas en el código:

                import { Injectable } from '@angular/core';
                import { Usuario } from '../../models/usuario.model';
                import { HttpClient } from '@angular/common/http';
                
Para no ir escribiendo la url de nuestro backend-server en todas las peticiones vamos a crear una variable **URL_SERVICIOS**
en un archivo de configuracion que export e importaremos en este archivo.

                import { URL_SERVICIOS } from '../../config/config';
                
Esta es una librería para hacer popup de alerta, y avisar al usuario de acciones.

                import swal from 'sweetalert';

Esta librería es para mapear las salidas que nos llegan del backend-server

                import { map } from 'rxjs/operators';
                
Usaremos el router para redirigirnos a otras páginas cuando se haga alguna petición.

                import { Router } from '@angular/router';

                @Injectable({
                  providedIn: 'root'
                })
                export class UsuarioService {

Definimos las variables donde guardaremos al usuario y el token.

                  usuario: Usuario;
                  token: string;

                  constructor(
                    public http: HttpClient,  
                    public router: Router) {

Cuando se inicie el servicio vamos a recoger al usuario y token del localStorage, 
por si ya hay un usuario.
                      this.cargarStorage();

                   }
                   
**Funcion**.Con esta función comprobamos que ya hay alguien logeado, siempre que tengamosun token en nuestra
variable, tenemos a un usuario logeado.

                   estaLogueado() {
                     return (this.token.length > 5) ? true : false;
                   }

**Funcion**. En esta función cargamos en nuestras variables lo que se encuentra en el LocalStorage

                   cargarStorage() {
                     if (localStorage.getItem('token')) {
                       this.token = localStorage.getItem('token');
                       this.usuario = JSON.parse(localStorage.getItem('usuario'));
                     } else {
                      this.token = '';
                      this.usuario = null;
                     }
                   }

**Funcion**. En esta función guardamos en el localStorage el usuario logeado. La manera que tenemos
de saber si un usuario está logeado en nuestra página es atraves del LocalStorage.

                  guardarStorage(id: string, token: string, usuario: Usuario) {
                    localStorage.setItem('id', id);
                    localStorage.setItem('token', token);
                    localStorage.setItem('usuario', JSON.stringify(usuario));
                    this.usuario = usuario;
                    this.token = token;
                  }
                  
**Funcion**. Para hacer un Logout lo unico que tenemos que hacer es borrar del localStorage los datos el usuario y el token.

                  logout() {
                    this.usuario = null;
                    this.token = '';

                    localStorage.removeItem('token');
                    localStorage.removeItem('usuario');

                    this.router.navigate(['/login']);

                  }

**Funcion - Conexión con Backend-Server**. Esta función va hacer un petición http a nuestro backend-server y poder logear 
a un usuario a través del token que Google nos proporciona. Al hacer la petición al Backend-Serve, este nos va devolver la misma salida que el POSTMAN nos muestras
y que hemos definidos en nuestras peticiones del lado de Node.

                  loginGoogle(token: string) {
                  
Construimos la ulr, tenemos que fijarnos, como la hemos definido en el Backend.

                    const url = URL_SERVICIOS + '/login/google';
                    
Hacemos la llamada http y le pasamos el token recogido por Google (este token lo hemos recogido en login.component.ts)
Si todo hay salido bien (los errores aún no los estamos recogiendo, solo se muestran en consola), esta petición nos devuelve
una **resp**, que es la misma que hemos estado biendo en el POSTMAN.

Con esta respuesta json que hemos definido en el Backend, vamos hacer un par de cosas:
- La primera es guardar el id , el tolen y al usuario en el localStorage
- Segundo es definir lo que esta petición va a devolver, en este caso es un true. Nada más.

                    return this.http.post(url, {token})
                      .pipe(map((resp: any ) => {
                          this.guardarStorage(resp.id, resp.token, resp.usuario);
                          return true;
                    }));
                  }
                  
**Funcion - Conexión con Backend-Server**.

                login(usuario: Usuario, recordar: boolean = false) {

                  if (recordar) {
                    localStorage.setItem('email', usuario.email);
                  } else {
                    localStorage.removeItem('email');
                  }

                  const url = URL_SERVICIOS + '/login';
                  return this.http.post(url, usuario)
                    .pipe(map((res: any ) => {

                      this.guardarStorage(res.id, res.token, res.usuario);
                      return true;
                    }));
                }

**Funcion - Conexión con Backend-Server**.

                  crearUsuario(usuario: Usuario) {

                    const url = URL_SERVICIOS + '/usuario';
                    // Para ser notificado cuando esto se haga vamos a decolver un observador al que nos vamos
                    // a poder subcribir.
                    return this.http.post(url, usuario)
                      .pipe(map( (res: any) => {

                        swal('Usuario creado', usuario.email, 'success');
                        return res.usuario;
                      }));

                  }
                }

 
 1. Crear los formularios
 2. Crear las validaciones
 4. Hacer que el formulario tenga su propio submit y llame a una funcion del componente.
    De momento esa funcion va a mostar por consola los datos del usuario que se acaba de registrar
 
 5. Crear un servicio nuevo usuario.service.ts y crear un método post que llame a nuestro backend, que está corriendo
 con la ruta que hemos definido. Para ello, tenemos que importar el HttpClient y en el module el HttpClientModule
 
 6. Injectar el nuevo servicio en el componente register y hacer que el submit llama la funcion del servicio
 y se subcriba a ella. Si todo lo hace bien, navegar
 
 
