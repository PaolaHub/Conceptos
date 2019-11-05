
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
                
 ## Conectado con el Backend-Server
 
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
                    
Hacemos la petición http y le pasamos el token recogido por Google (este token lo hemos recogido en login.component.ts)
Si todo ha salido bien (los errores aún no los estamos recogiendo, solo se muestran en consola), esta petición nos devuelve
una **resp**, que es la misma que hemos estado biendo en el POSTMAN. Con esta respuesta json que hemos definido en el Backend, vamos hacer un par de cosas:

- La primera es guardar el id , el token y al usuario en el localStorage
- Segundo es definir lo que esta petición va a devolver un observable, en este caso es un true. Nada más. Está función devuelve un observable al que vamos a tener que subcribirnos.

                    return this.http.post(url, {token})
                      .pipe(map((resp: any ) => {
                          this.guardarStorage(resp.id, resp.token, resp.usuario);
                          return true;
                    }));
                  }
                  
**Funcion - Conexión con Backend-Server**.

Aquí vamos a logear a un usuario, vamos a recibir al usuario que vendrá de un formulario y recibimos también,
si queremos que el usuario se recuerde para no volver a escribir la dirección.

                login(usuario: Usuario, recordar: boolean = false) {

Si el usuario quiere recordar el e-mail, lo vamos a guardar en el localStorage.
Como hemos visto más arriba, cuando el servicio se inicia, se carga el localStorage y si encontramos
el email, va aparcer en este caso en el formulario.

                  if (recordar) {
                    localStorage.setItem('email', usuario.email);
                  } else {
                    localStorage.removeItem('email');
                  }
                  
 Vamos a contruir la url tal como la definimos en el Backend-Server.

                  const url = URL_SERVICIOS + '/login';
      
Hacemos la petición http y le pasamos como parámetro al usuario (recogido desdee el formulario). Esta petición nos devuelve
una **resp**, que es la misma que hemos estado viendo en el POSTMAN.

 Con esta respuesta json que hemos definido en el Backend, vamos hacer un par de cosas:
- La primera es guardar el id , el tolen y al usuario en el localStorage
- Segundo es definir lo que esta petición va a devolver, en este caso es un true. Nada más. Está función devuelve un observable al que vamos a tener que subcribirnos.

                  return this.http.post(url, usuario)
                    .pipe(map((res: any ) => {

                      this.guardarStorage(res.id, res.token, res.usuario);
                      return true;
                    }));
                }

**Funcion - Conexión con Backend-Server**.

Aquí vamos a crear un usuario nuevo.

                  crearUsuario(usuario: Usuario) {

 Vamos a construir la url tal como la definimos en el Backend-Server.
 
                    const url = URL_SERVICIOS + '/usuario';
                    
Hacemos la petición http para conectarnos con el Backend-Server y le pasamos como parámetro al usuario (recogido desdee el formulario). Esta petición nos devuelve una **resp**, que es la misma que hemos estado viendo en el POSTMAN.

Con esta respuesta json que hemos definido en el Backend, vamos hacer un par de cosas:
- La primera es mostrat un popup al usuario, diciendole que el usuario se ha creado.
- Segundo es definir lo que esta petición va a devolver, en este caso devolvermos al usuario. Nada más. Está función devuelve un observable al que vamos a tener que subcribirnos.

                    // Para ser notificado cuando esto se haga vamos a devolver un observador al que nos vamos
                    // a poder subscribir.
                    return this.http.post(url, usuario)
                      .pipe(map( (res: any) => {
                        swal('Usuario creado', usuario.email, 'success');
                        return res.usuario;
                      }));

                  }
                }

 ## Llamar a las peticiones del servico.
 
Como ya sabemos, para poder trabajar con este servicio, hay que injectarlo en el componente que deseemos.
En nuestro caso, vamos a injectarlo en el componente login y register.
Casa vez que el usuario, le de a el botón **"Ingresar" o "Crear nueva cuenta"** vamos a llamar en el **submit**,
a las funciones de nuestro servicio.

### register.component.ts

Injectamos nuestro servicio en el constructor

              constructor(
                // tslint:disable-next-line: variable-name
                public _usuarioService: UsuarioService,
                public router: Router
              ) { }
  
En la funcion **submit**, llamamos a las funciones de nuestro servicio.

              registrarUsuario() {

                if (this.forma.invalid) {
                    return;
                }

                if (!this.forma.value.condiciones) {
                  swal('Importante!', 'Debe de aceptar las condiciones!', 'warning');
                  console.log('Debe de aceptar las condiciones');
                  return;
                }
                
Crea al usuario, desde elformulario

                const usuario = new Usuario(
                  this.forma.value.nombre,
                  this.forma.value.correo,
                  this.forma.value.password
                );

Llama a la funcion **crearUsuario** pasandole el usuario.
Como la función nos devuelve un observable, hay que subscribirse.
Cuando la peticón termina, nos va avisar y en la **resp** tendremos al usuario, aunque no vamos hacer nada con él.
No único que hacemos es redirigirnos a la página de login, para que el usuario pueda hacer el login.

                // Esto no se va a disparar a menos que nos subcribamos
                this._usuarioService.crearUsuario(usuario)
                // Todo lo que el postman devuelve en el "res", es lo que está dentro del resp.
                .subscribe(resp => this.router.navigate(['/login']));
              }
 
### login.component.ts 

              ingresar(forma: NgForm) {

                if (forma.invalid) {
                  return;
                }

Crea al usuario, desde elformulario

                const usuario = new Usuario(null, forma.value.email, forma.value.password);

Llama a la funcion **login** pasandole el usuario y si quiere que lo recuerde, para guaradar el email en el localStorage.
Como la función nos devuelve un observable, hay que subscribirse.
Cuando la peticón termina, nos va avisar y en la **resp** tendremos un true, aunque no vamos hacer nada con él.
No único que hacemos es redirigirnos a la página principal de la app.

                this._usuarioService.login(usuario, forma.value.recuerdame).subscribe( resp => this.route.navigate(['/dashboard']));
              }

## Guards

Los guard nos ayudan a proteger nuestras rutas.
Lo que queremos hacer aquí es mostrar como si un usuario no está logeado, no va poder acceder a la app, solo al login, para que se logee.

### Creamos un guard

¿Donde se colocan? Un Guard tambíen es como un servicio. Es por ello, que vamos a crearlo en una carpeta dentro 
delos servicios.

**ng g g services/guards/login => Creamos el LoginGuard**

### Definimos el guard

Lo más importante aquí es la función **CanActivate**, que va devolver si el Guard deja pasar o bloquea el acceso.
Para ello, tenemos que ver si hay en el localStorage un token definido. Es por eso, que necesitamos injectar
nuestro servicio **UsuarioService**.

            import { Injectable } from '@angular/core';
            import { CanActivate, Router } from '@angular/router';
            import { Observable } from 'rxjs';
            import { UsuarioService } from '../usuario/usuario.service';

            @Injectable({
              providedIn: 'root'
            })
            export class LoginGuard implements CanActivate {

              constructor(
                public _usuarioService: UsuarioService,
                public router: Router
              ) {
              }

Lo que vamos hacer es simplemente llamar a la función **estaLogueado** de nuestro servicio.
Si es así, devuelve un true. Si no, nos va a redirigir a la página login y devuelve un false.

              canActivate() {
                if (this._usuarioService.estaLogueado()) {
                  console.log('Paso por el Login Guard');
                  return true;
                } else {
                  console.log('Bloqueado por el Guard');
                  this.router.navigate(['/login']);
                  return false;
                }
              }
            }
            
### Donde usamos el Guard?

Los Guard se usan para proteger las routes, entonces los vamos a llamar en nuestros archivos de rutas.
Simplemente, añadiendo este parámetro: **canActivate: [LoginGuard],**

            const pagesRoutes: Routes = [
                { 
                    path: '',
                    component: PagesComponent,
                    canActivate: [LoginGuard],
                    children: [
                        { path: 'dashboard', component: DashboardComponent, data: { titulo: 'Dashboard'} },
                        { path: 'progress', component: ProgressComponent, data: { titulo: 'Progress'} },
                        { path: 'graficas1', component: Graficas1Component, data: { titulo: 'Graficas'} },
                        { path: 'promesas', component: PromesasComponent, data: { titulo: 'Promesas'} },
                        { path: 'rxjs', component: RxjsComponent, data: { titulo: 'RxJs'} },
                        { path: 'account-settings', component: AccountSettingsComponent, data: { titulo: 'Ajustes del tema'} },
                        { path: '', redirectTo: '/dashboard', pathMatch: 'full'}
                    ]
                }
            ];
