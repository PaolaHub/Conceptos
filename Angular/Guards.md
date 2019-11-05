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
