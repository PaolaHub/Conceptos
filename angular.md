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









