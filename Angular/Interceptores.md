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
