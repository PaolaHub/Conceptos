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
