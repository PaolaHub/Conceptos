# ANGULAR

## Input and Output
El input y el output se utilizan para mandar información de componentes padres a hijo y viceversa.
#### Input - Para recibir datos

En el hijo se utiliza el módulo Input del core => import { Input } from '@angular/core';

Y se declara así => @Input() recibeDelPadre:string;

El intercambio de realiza desde la etiqueta al ser usuada => <app-hijo [recibeDelPadre]="variable"></app-hijo>

#### Output - Para mandar datos

En el hijo se necesita importar => import { Output, EventEmitter } from '@angular/core';

Y se declara así => @Output() servicioSeleccionado: EventEmitter<number>;

En el constructor lo inicializamos => this.servicioSeleccionado = new EventEmitter();

Luego hay que lanzar el evento para que el padre lo escuche en cualquier función que queramos =>
this.servicioSeleccionado.emit(this.index);

Para que el padre lo escuche tenemos que definirlo al llamar a la etiqueta hija
<app-hijo (servicioSeleccionado)="verServicio($event)" [recibeDelPadre]="variable"></app-hijo>
por supuesto el verServivio($event) tiene que ser definido en el padre.

## Modulos y rutas hijas

El app.module.ts no debe ser muy largo. El objetivo es tener archivos ligeros
y facil de entender y mantener.
Para ello se pueden crear diferentes módulos agrupandolos según su finalidad y relacionarlos.
Por ejemplo, si nuestra App tiene diferentes páginas, componentes, componentes compartidos.
Podemos hacer para cada uno de ellos su módulo independiente, y no tenerlo todo en el app.module.ts

Cada componente está declarado en un módulo. Y cada módulo juega de manera independiente.
Por ello tenemos que:
  - Declarar (declarations: []) los componentes que componen ese módulo.
  - Importar (imports: []) otros componentes o rutas que sean necesarias de otros módulos.
  - Exportar (exports: []) los componentes del módulo que queremos que otros módulos usen.

Una vez que creamos el módulo, hay que añadirlo en las importaciones del app.component
o del módulo que quiera usarlo. Recordar que los módulos siempre van en la parte de IMPORT.

Lo mismo hay que hacer con las rutas.
El app.routes siempre contiene la ruta principal (forRoot)
  
  - export const APP_ROUTES = RouterModule.forRoot(appRoutes, {useHash: true});
  
Y las rutas secundarias se marcan con forChild:

 - export const PAGES_ROUTES = RouterModule.forChild(pagesRoutes);
 
 > (Ver más en Curso Angular Avanzado: Fernando Herrera Section 3 y 4)
 
### Promesas

Las promesas llevan una función de callback, con dos parámetros:
1. Resolver, para cuando la promesa haya terminado.
2. Reject, cuando se produce algún error.

Declaración de un promesa:
 
      let promesa = new Promise((resolve, reject) => {

        let contador = 0;
        let intervalo = setInterval(()=>{

          contador += 1;
          console.log(contador);

          if(contador === 3){

            resolve(true);
            clearInterval(intervalo);
          }
          
        }, 1000)
      });
      
Llamada a una promesa:
1. Then: Si la promesa ha terminado bien y se llamo al método resolver.
2. Catch: Si la promesa acabó mál y se llamó al método reject.

    promesa.then(
      mensaje => console.log('Termino!', mensaje)
    )
    .catch(
      error => console.log('Error en la promesa', error));
      
Normalmente, las promesas van definidas en una función:

    contarTres(): Promise<boolean>{
    
    return new Promise((resolve, reject) => {

      let contador = 0;
      let intervalo = setInterval(()=>{

        contador += 1;
        console.log(contador);

        if(contador === 3){

          resolve(true);
          clearInterval(intervalo);

        }
      }, 1000)
    });
    }
    
Y se les llama así:
    
    this.contarTres().then(
      mensaje => console.log('Termino!', mensaje)
    )
    .catch(
      error => console.log('Error en la promesa', error));
 
### Observables

Los Observable no están definidos en el ECMAScript6, por lo tanto hay que importarlos.
**import { Observable, Subscriber } from 'rxjs';** ReactiveX extensions.

Los Observable son como las promesas, pero con más funcionalidades:
No tienen un método resolve y reject como las promesas, si no solo un parámetro observables.
El parámetro observable tiene varias funciones, una de ellas es el:
* **observable.next()**. Esta función manda parámetros mientras esté subscrito. (**observable.next(contador)**).
* **observable.complete()**. Para decirle al observador que deje de escuchar (que no siga subscrito que ya ha terminado).
Esta función no manda ningún parámetro, solo avisa que ya ha terminado su propósito.

Declaración de un observable:
 
     let obs = new Observable( (observer: Subscriber<any>) => {

        let contador = 0;

        let intervalo = setInterval(
          () => {

            contador += 1;
            // Vamos mandándole datos.
            observable.next(contador);
            if(contador == 3){
              // Así paramos el intervalo.
              clearInterval(intervalo);
              // Así se para la subscripción para dejar de escuchar.
              observable.complete();
            }

            if(contador == 2){
              //clearInterval(intervalo);
              observable.error('Auxilio!')
            }
          }, 1000)

    });
    
Subscription a un observable.
Los observables tienen tres callback:
1. Para ir mandado información
2. Por si hay algún error, en este caso la subscripción se para.
3. Para avisar que ya ha terminado.

Si se produce algún error, y queremos que se subscriba otra vez,
tenemos un método que se llama **retry**. Este método tiene que importarse de **import {retry} from rxjs/operators**.
Para que funcione, tiene que ser llamado dentro de un pipe, como en el ejempo de abajo.

    // Los observables tienen tres callback !
    obs.pipe(
      retry(2)
    )
    .subscribe(
        // Cuando se llama a un next para mandale información mientras escucha.
        numero => console.log("Subs ", numero),
        // Cuando hay un error.
        error => console.error('Error en el obs', error),
        // Cuando el observador termino.
        () => console.log('El observador termino')
     );

Lo mismo que con las Promesas, normalmente los Observables, están definidos dentro de una funcion:

regresaObservable(): Observable<number>{
  return ...Observable...
  }


### Operador Map
Nos podemos imaginar un aspersor de agua, donde nos llega agua por un lago pero podemos
manejar como querremos que salga el agua, como un chorro, como aspersor, más presión, menos presión.
Pues eso es un operador map, no es mas que transformar la información que ya tenemos.
Es la misma información que yo estoy recibiendo pero expresada de otra manera.

Para usarlo, tenemos que importarlo de rxjs/operators
**import { map } from 'rxjs/operators';**

Nuestro observable está devolviendo un objeto llamado salida, 
pero a nosotros no nos interesa el objeto salida, si no el valor que contiene
dentro, es por ello que lo pasamos por un pipe usando el map.
El operador map, nos permite transformar la información.

    regresaObservable(): Observable<any>{
    
    return new Observable( (observer: Subscriber<any>) => {

      let contador = 0;

      const intervalo = setInterval(
        () => {

          contador += 1;

          const salida = {
            valor: contador
          };

          // Vamos mandándole datos.
          observer.next(salida);

          if(contador == 3){
            // Así paramos el intervalo.

            clearInterval(intervalo);
            // Así se para la subscripción para dejar de escuchar.
            observer.complete();
          }

          // if(contador == 2){
          //   //clearInterval(intervalo);
          //   observer.error('Auxilio!')
          // }
        }, 1000)
      }).pipe(
        // map(resp => { return resp.valor})
        map(resp => resp.valor)
      )
      }


### Operador Filter

El operador filter es como un interruptor, va a filtrar información.
Va a devolver un true o un false, True deja pasar la información, False ignora la información.
Tiene dos argumentos que son el propio valor que le llega del observable y el index, que
son las veces que se ha llamado al operador.
En este ejemplo, como nuestro observable nos está devolviendo numeros,
hemos echo un filtro para que solo nos devuelva los números impares:

    regresaObservable(): Observable<any>{
    
      return new Observable( (observer: Subscriber<any>) => {

      let contador = 0;

      const intervalo = setInterval(
        () => {

          contador += 1;

          const salida = {
            valor: contador
          };

          // Vamos mandándole datos.
          observer.next(salida);

          if(contador == 3){
            // Así paramos el intervalo.

            clearInterval(intervalo);
            // Así se para la subscripción para dejar de escuchar.
            observer.complete();
          }

          // if(contador == 2){
          //   //clearInterval(intervalo);
          //   observer.error('Auxilio!')
          // }
        }, 1000)
      }).pipe(
        // map(resp => { return resp.valor})
        map(resp => resp.valor),
        filter( (valor, index) => {
          
          if(valor % 2 === 1) {
            return true;
          }
          else  {
            return false;
          }
        })
      )
      }
      
Más sobre los diferentes operadores disponibles de RXJS - Operators

http://reactivex.io/documentation/operators.html

### Llamar al unsubscribe

Para parar a los observables cuando se sale del componente,
podemos llamar a la funcion unsubscribe cuando el componente se destruye:
Para eso tenemos que importar el **import { OnDestroy } from '@angular/core'**.

Dentro de la clase vamos a crear una variable Subscription,
y se la vamos a asignar a la llamada al Observable.

Luego vamos a llamar al unsubscribe en el OnDestroy.

    export class RxjsComponent implements OnInit, OnDestroy {
     
     subscription: Subscription;
     
     constructor() {

      this.subscription = this.regresaObservable()
      .subscribe(
        numero => console.log("Subs ", numero),
        error => console.error('Error en el obs', error),
        () => console.log('El observador termino')
      );
     }
    
     ngOnDestroy() {
      console.log("La página se va a cerrar");
      this.subscription.unsubscribe();
     }
    }
 

### Usando Observable para obtener la data del router.

Al router puede configurarsele unos datos, los que querramos.

**{ path: 'dashboard', component: DashboardComponent, data: { titulo: 'Dashboard'} },**

El objeto router, tiene un observable: **events**. Para saber lo que va pasando por las rutas.
Si hacemos un console.log(events) de los datos que nos proporciona el observable,
tenemos el **data** que hemos definido en las routes.
Con los operadores Filter y Maps sacamos esa **data** y nos subscribimos al objeto.
El objecto que nos llega del observable al subscribirnos, será exactamente la información **data**,
que estamos buscando.

        import { Component, OnInit } from '@angular/core';
        import { Router, ActivationEnd } from '@angular/router';
        import { filter, map } from 'rxjs/operators';

        @Component({
          selector: 'app-breadcrums',
          templateUrl: './breadcrums.component.html',
          styles: []
        })
        export class BreadcrumsComponent implements OnInit {

        titulo: string;

          constructor(private router: Router) { 

            this.getDataRouter()
            .subscribe(
              data => {
                this.titulo = data.titulo;

              }
            )
          }

          ngOnInit() {
          }

          getDataRouter()
          {
            return this.router.events.pipe(
                filter(evento => evento instanceof ActivationEnd),
                filter((evento: ActivationEnd) => evento.snapshot.firstChild === null),
                map( (evento:ActivationEnd) => evento.snapshot.data)
            );
          }

        }


### 82. MetaTags, Título y Página actual

Hay dos injectable definidos en Angular,
que nos permiten cambiar el titulo de la página en la pestaña del navegador
y otra que nos permite crear meta tags, para ayudar al navegador en sus busquedas.

Son dos servicios injectables: Title y Meta
Cada vez que se produce un cambio en la ruta, está cambiando el nombre de la pestaña
y creando un metaTag con el data del observable.

    constructor(private router: Router,
      private title: Title,
      private meta: Meta) { 

      this.getDataRouter()
      .subscribe(
        data => {
          this.titulo = data.titulo;
          this.title.setTitle(this.titulo);

          const metaTag: MetaDefinition = {
              name: 'description',
              content: this.titulo
          };

          this.meta.updateTag(metaTag);
        }
      )
    }
