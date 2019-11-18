# Interceptores
    
Vamos a creanos un interceptor que sea capaz de atrapar esta petición http 
o cualquier peticion que salga de este servicio y a la vez, me coloque el token
que mandabamos como headers en el ejemplo sin interceptores.

Además, vamos a manejar los errores desde ahí.

## ¿Qué son los interceptores?

Los interceptores no son más que un servicio corriente. 
Por ello usamos el mismo comando **ng g s interceptors/nombreInterceptor** para crearlos y los agruparemos
en una carpeta que se llame interceptors.
Una vez creado solo hay que hacer dos cosas:

1. Hacer que el la clase del Interceptor herede de un HttpInterceptor.

        export class InterceptorService implements HttpInterceptor {

2. Definir el Interceptor en el APP.module. 
  Decirle al APP.module que ahora tiene este interceptor y que lo eche a andar y que lo ponga a escuchar todas las peticiones.
  
    Así se configuran dos interceptors:
    Se pueden crear tantos como quieran.
    Incluso podemos crear un modulo con todos los interceptores que necesitemos,
    para que App.module quede bastante limpio.

    providers: [
    {
      provide: HTTP_INTERCEPTORS,
      useClass: InterceptorService,
      multi: true
    },
    {
      provide: HTTP_INTERCEPTORS,
      useClass: OtroService,
      multi: true
    },
    
NOTA. Vemos como el servicio interceptor no hay que inyectarlo en ningún construtor.

# A continuación dejamos los ejemplos

## usuario.service.ts

        import { Injectable } from '@angular/core';
        import { HttpClient, HttpParams, HttpHeaders, HttpErrorResponse } from '@angular/common/http';
        import { map, catchError } from 'rxjs/operators';
        import { throwError } from 'rxjs';
        import { tokenName } from '@angular/compiler';
        import { headersToString } from 'selenium-webdriver/http';

        @Injectable({
          providedIn: 'root'
        })
        export class UsuariosService {

          constructor(private http: HttpClient) { }

          obtenerUsuario() {

            // *****************
            // SIN INTERCEPTORES
            // *****************

            // let params = new HttpParams().append('page', '2');
            // params = params.append('nombre', 'Paola');

            // const headers = new HttpHeaders({
            //   'token-usuario': 'ABC938238434dsdfsdfsdf'
            // });

            // return this.http.get('https://reqres.in/api/user', {
            //   params, headers
            // }).pipe(
            //   map(resp => resp['data']),
            //   catchError(this.manejarError)
            // );

            // *****************
            // CON INTERCEPTORES
            // *****************
            // Vamos a creanos un interceptor que sea capaz de atrapar esta petición http 
            // o cualquier peticion que salga de este servicio y a la vez, me coloque el token
            // que mandabamos como headers en el ejemplo sin interceptores.

            // Los interceptores no son más que un servicio corriente. 
            // Por ello usamos el mismo comando para crearlos y los agruparemos
            // en una carpeta que se llame interceptors.
            // Lo unico que hay que hacer es que la clase sea implementada por un HttpInterceptor

            let params = new HttpParams().append('page', '2');
            params = params.append('nombre', 'Paola');

            return this.http.get('https://reqres.in/api/user', { params }).pipe(
              map(resp => resp['data'])
            );

          }

          manejarError(error: HttpErrorResponse) {
            console.log('Sucedió un error');
            console.log('Registrado en el log file');
            console.warn(error);
            return throwError('Error personalizado');
          }
        }
        
## app.component.ts

    import { Component } from '@angular/core';
    import { UsuariosService } from './services/usuarios.service';

    @Component({
      selector: 'app-root',
      templateUrl: './app.component.html',
      styleUrls: ['./app.component.css']
    })
    export class AppComponent {

        constructor(private usuarioService: UsuariosService) {

          this.usuarioService.obtenerUsuario().subscribe( resp => {
            console.log(resp);
          }, (err) => {
            console.log('Erro en el App component');
          });
        }
    }
    
## interceptor.service.ts

        import { Injectable } from '@angular/core';
        import { HttpInterceptor, HttpRequest, HttpHandler, HttpEvent, HttpHeaders, HttpErrorResponse } from '@angular/common/http';
        import { Observable, throwError } from 'rxjs';
        import { catchError } from 'rxjs/operators';

        @Injectable({ providedIn: 'root'})
        export class InterceptorService implements HttpInterceptor {

          constructor() { }

          intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
            // Return de la misma req para que el interceptor deje pasar todo
            // Es como que tengamos una válvula abierta. Todo lo que pasa por el http
            // entraría por el INTERCEPTOR y seguiría fluyendo.
            // No hace nada por el momento, los está viendo y los está dejando pasar con el next.
            console.log('Paso por el interceptor');

            const headers = new HttpHeaders({
              'token-usuario': 'ABC938238434dsdfsdfsdf'
            });

            /*
            Cuando utilizamos la req, ésta ya deja de poder usarse, es como si inmutara,
            y ya no se puede volver a utilizar para hacer una petición, por lo cual tenemos que
            clonarla y tenemos que clonarla antes que sea manipulada.
            Porque una req que ya se manipula, no la vamos a poder volver a llamar.
             */
            const reqClone = req.clone({ headers });

            return next.handle(reqClone).pipe(
              catchError(this.manejarError)
            )
          }

          manejarError(error: HttpErrorResponse) {
            console.log('Sucedió un error');
            console.log('Registrado en el log file');
            console.warn(error);
            return throwError('Error personalizado');
          }
        }


## app.module.ts

        import { BrowserModule } from '@angular/platform-browser';
        import { NgModule } from '@angular/core';
        import { HttpClientModule, HTTP_INTERCEPTORS } from '@angular/common/http';

        import { AppComponent } from './app.component';
        import { InterceptorService } from './interceptors/interceptor.service';

        @NgModule({
          declarations: [
            AppComponent
          ],
          imports: [
            BrowserModule,
            HttpClientModule
          ],
          providers: [
            {
              provide: HTTP_INTERCEPTORS,
              useClass: InterceptorService,
              multi: true
            }
          ],
          bootstrap: [AppComponent]
        })
        export class AppModule { }





  
  
