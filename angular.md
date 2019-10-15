# ANGULAR

## Input and Output
El input y el output se utilizan para mandar información de componentes padres a hijo y viceversa.
### Input - Para recibir datos

En el hijo se utiliza el módulo Input del core => import { Input } from '@angular/core';

Y se declara así => @Input() recibeDelPadre:string;

El intercambio de realiza desde la etiqueta al ser usuada => <app-hijo [recibeDelPadre]="variable"></app-hijo>

### Output - Para mandar datos

En el hijo se necesita importar => import { Output, EventEmitter } from '@angular/core';

Y se declara así => @Output() servicioSeleccionado: EventEmitter<number>;

En el constructor lo inicializamos => this.servicioSeleccionado = new EventEmitter();

Luego hay que lanzar el evento para que el padre lo escuche en cualquier función que queramos =>
this.servicioSeleccionado.emit(this.index);

Para que el padre lo escuche tenemos que definirlo al llamar a la etiqueta hija
<app-hijo (servicioSeleccionado)="verServicio($event)" [recibeDelPadre]="variable"></app-hijo>
por supuesto el verServivio($event) tiene que ser definido en el padre.





