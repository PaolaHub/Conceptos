# Flexbox

Un entorno flexbox permite agrupar fácilmente un conjunto de cajas de diversas maneras/posiciones, ahorrandonos mucho en código.

## Entorno

Para crear un entorno Flexbox, hay que crear un objeto con el display: flex

        .entorno {
          display: flex;
        }

        <div class="entorno">
                // Todos los elementos definidos aquí, se agruparan uno detrás de otro, ignorando la
                // propiedad block de cada elemento.
        </div>
           
Para ahorrarnos definir el código csss, bootstrap nos proporciona la clase d-flex

        <div class="d-flex">
             // Todos los elementos definidos aquí, se agruparan uno detrás de otro, ignorando la
             // propiedad block de cada elemento.
            <div class="item2">Col 2</div>
            <div class="item3">Col 3</div>
            <div class="item4">Col 4</div>
        </div>
        
Comportamiento responsive: **d-md-flex**

## Orientación (row or column)

Por defecto los elemntos se orientan de manera horizontal (row) uno detrás de otro, pero también podemos hacer que se alineen, uno por debajo de otro, orientación vertical, en este caso cada elemento ocupará toda la anchura del padre.
Para echo tenemos en css la propiedad **flex-direccion** o en bootstrap **flex-column**.

        .entorno {
          display: flex;
          flex-direction column;
        }
        
ó ahorrando código:

        <div class="d-flex flex-column">
            <div class="item2">Col 2</div>
            <div class="item3">Col 3</div>
            <div class="item4">Col 4</div>
        </div>

## Alineación en el eje principal ( Sobre el eje horizontal )

Los hijos pueden alinearse a la derecha a la izq. al centro con espacio entre ellos, etc..
Esto lo podemos hcaer con la propiedad csss **justify-content**.
Esto hace que todos los hijos que se encuentra dentro de un objeto con este clase definida,
van a agruparse en el centro

        .entorno {
          display: flex;
          justify-content: center; /* rigth, left, between, ... */
        }
        
La clase definida ya en Bootstrap es **justify-content-**

        <div class="d-flex justify-content-center">
            <div class="item2">Col 2</div>
            <div class="item3">Col 3</div>
            <div class="item4">Col 4</div>
        </div>
        
Comportamiento responsive: **justify-content-md-center**

## Alineación en el eje secundario ( Sobre el eje vertical )

Los hijos pueden alinearse ocupando todo la altura del padre, pueden alinearse arriba, en el centro o abajo.
Esto lo podemos hcaer con la propiedad csss **align-items**.

        .entorno {
          display: flex;
          align-items: stretch (ocupa toda la altura del padre); 
           /* flex-end (abajo), flex-start (arriba), center (de centrar de manera vertical) */
        }
        
La clase definida ya en Bootstrap es **align-items-** start, center, end, stretch
Tenemos: align-items-start / align-items-center / align-items-end  / align-items -stretch

        <div class="d-flex align-items-center"> 
            <div class="item2">Col 2</div>
            <div class="item3">Col 3</div>
            <div class="item4">Col 4</div>
        </div>
        
Comportamiento responsive: **align-items-sm-start**

## Alineación individual de los hijos en el eje secundario

Normalmente se le aplica al padre y afeca a todos los hijos.
Pero que pasa si nosotros quisieramos una alineación de un hijo determinado.

**.align-seft-start / .align-seft-center / .align-seft-end / .align-seft-stretch**


        <div class="d-flex align-items-center"> 
            <div class="item2">Col 2</div>
            <div class="item3">Col 3</div>
            <div class="item4 align-seft-start">Col 4</div>
        </div>
        
Comportamiento responsive: **align-seft-sm-start**

## La magia de Flex-fill

Hijos flexibles. Esta clase se le aplica a los hijos.
Esta clase hace que los elementos no ocupen solo el espacio de su contenido, sino que aprovechen todo el espacio 
del padre.

        <div class="d-flex align-items-center"> 
            <div class="item2 flex-fill">Col 2</div>
            <div class="item3 flex-fill">Col 3</div>
            <div class="item4 flex-fill">Col 4</div>
        </div>
