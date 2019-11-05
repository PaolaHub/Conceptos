# Formularios en Angular

En Angular podemos implementar dos tipos de formulario: **Por Template y Reaktiv Form**.

Vamos a poner un ejemplo con dos formulario. Uno en el que un usuario se registra a una aplicación y
otro de como se logea.

## Reaktiv form - Register Form

### En el hmtl:

Hay que decile a Angular que ese formulario va ser tratado como un Reaktivform.

Le definimos el **[formGroup]** que será una referencia al formulario y tratamos el **Submit**,
en vez de dejarlo en un botón con type="submit".

            <form ngNativeValidate [formGroup]="forma" (ngSubmit)="registrarUsuario()"
            
Con el **ngNativeValidate** le estamos diciendo a Chrom que trate las validaciones que le definamos.

A cada entada hay que definirle un **formControlName** y un **name**.

            <input formControlName="nombre" name="nombre" class="form-control" type="text" required placeholder="Nombre">
            <input formControlName="correo" name="correo" class="form-control" type="text" required placeholder="Correo">
            <input formControlName="password" name="password" class="form-control" type="password" required placeholder="Contraseña">
            <input formControlName="password2" name="password2" class="form-control" type="password" required placeholder="Confirmar contraseña">
            
Al haber definido el submit en la etiqueta del form, le estamos diciendo a Angular que trate a este
formulario como un Reaktivform y cuando se encuentre otro submit en algún botón, lo va a ignorar.

Un ejemplo:

            <form ngNativeValidate [formGroup]="forma" (ngSubmit)="registrarUsuario()" class="form-horizontal form-material"        id="loginform" action="index.html">
                <a href="javascript:void(0)" class="text-center db"><img src="assets/images/logo-icon.png" alt="Home" /><br/><img src="assets/images/logo-text.png" alt="Home" /></a>
                <h3 class="box-title m-t-40 m-b-0">Regístarte ahora</h3><small>Crea una cuenta y disfruta</small>
                <div class="form-group m-t-20">
                    <div class="col-xs-12">
                        <input formControlName="nombre" name="nombre" class="form-control" type="text" required placeholder="Nombre">
                    </div>
                </div>
                <div class="form-group ">
                    <div class="col-xs-12">
                        <input formControlName="correo" name="correo" class="form-control" type="text" required placeholder="Correo">
                    </div>
                </div>
                <div class="form-group ">
                    <div class="col-xs-12">
                        <input formControlName="password" name="password" class="form-control" type="password" required placeholder="Contraseña">
                    </div>
                </div>
                <div class="form-group">
                    <div class="col-xs-12">
                        <input formControlName="password2" name="password2" class="form-control" type="password" required placeholder="Confirmar contraseña">
                    </div>
                </div>
                <div class="form-group" *ngIf="forma.errors?.sonIguales && !forma.pristine">
                    <p class="text-danger">Las contraseñas deben ser iguales</p>
                </div>
                <div class="form-group row">
                    <div class="col-md-12">
                        <div class="checkbox checkbox-primary p-t-0">
                            <input formControlName="condiciones" name="condiciones" id="checkbox-signup" type="checkbox">
                            <label for="checkbox-signup"> Estoy de acuerdo con los <a href="#">Téminos</a></label>
                        </div>
                    </div>
                </div>
                <div class="form-group text-center m-t-20">
                    <div class="col-xs-12">
                        <button class="btn btn-info btn-lg btn-block text-uppercase waves-effect waves-light" type="submit">Registrarme</button>
                    </div>
                </div>
                <div class="form-group m-b-0">
                    <div class="col-sm-12 text-center">
                        <p>¿Tienes una cuenta? <a routerLink="/login" class="text-info m-l-5"><b>Ingresa ahora</b></a></p>
                    </div>
                </div>
            </form>


### En el component.ts

Es importante importar lo siguiente, para que nos funcione:

            import { FormGroup, FormControl, Validators } from '@angular/forms';

Vamos a definir en la clase un FormGroup con el mismo nombre al que definimos en el **hmtl**.

            forma: FormGroup;
            
En el OnInit vamos a definir al formularion y lo maquetamos:

Forma es un FormGroup, donde como primer paámetro se definen las campos del formulario (su valor, si es requerido, etc)
y como segundo parámetro podemos definirle validaciones personalizadas.

                // Definición y maquetación del formulario
                this.forma = new FormGroup({
                  nombre: new FormControl(null, Validators.required),
                  correo: new FormControl(null, [Validators.required, Validators.email]),
                  password: new FormControl(null, Validators.required),
                  password2: new FormControl(null, Validators.required),
                  condiciones: new FormControl(false)
                  
Vemos como en la siguiente línea se una **validación personalizada**

                }, {validators: this.sonIguales('password', 'password2') });
                
Tenemos que crer una **validación personalizada**, para asegurarnos que las dos contraseñas introducidas con iguales.
Para ello, creamos una funcion, de esta manera:

La función va a recibir en este ejemplo dos campos, las dos contraseñas, y tiene que devolver una funcion callback.
Donde recibe el formulario y devuelve null, si no son iguales o el mismo nombre de la funcion a true.
Es un poco peculiar veamos un ejemplo:


              sonIguales(campo1: string, campo2: string) {
                  return (group: FormGroup) => {

                    const pass1 = group.controls[campo1].value;
                    const pass2 = group.controls[campo2].value;

                    if (pass1 === pass2) {
                      return null;
                    }

                    return {
                      sonIguales: true
                    };
                  };
              }
                
Ahora definimos la función del submit:

              registrarUsuario() {

this.forma está referenciado con el formulario del hmtl. Así que tenemos ahí toda la información.

                if (this.forma.invalid) {
                    return;
                }
                
Aquí le estamos diciendo que si no acepta las condiciones del formulario, no puede registrarse

                if (!this.forma.value.condiciones) {
                  swal('Importante!', 'Debe de aceptar las condiciones!', 'warning');
                  console.log('Debe de aceptar las condiciones');
                  return;
                }
                
Cuando ya sabemos que el formulario es válido, creamos a un usuario con los datos del formulario.

                const usuario = new Usuario(
                  this.forma.value.nombre,
                  this.forma.value.correo,
                  this.forma.value.password
                );
                
 Y llamamos a nuestro servicio, que creara unnuevo usuario en nuestra base de datos.

                // Esto no se va a disparar a menos que nos subcribamos
                this._usuarioService.crearUsuario(usuario)
                // Todo lo que el postman devuelve en el "res", es lo que está dentro del resp.
                .subscribe(resp => this.router.navigate(['/login']));
              }
              
### Conclusión
Con el Reaktiv form, definimos el formulario en el **.ts** y nos evitamos que nuestro **html** sea demasiado engorroso.
Este método es bueno para formularios grandes.

## Por Template - Login Form

Vamos a usuar un formulario de login para este ejemplo

### En el hmtl

Para usar el formulario por template tenemos que definir una variable en la etiqueta **<form>**.
            
            <form ngNativeValidate #f="ngForm" class="form-horizontal form-material" (ngSubmit)="ingresar(f)" id="loginform" action="index.html">
            
Esta variable es **#f** de tipo **ngForm**. Como no vamos a tener una referencia, como en el caso del Reaktiv Form,
tenemos que pasarle esa variable f a la función que hacer el submit, es por eso que definimos **(ngSubmit)="ingresar(f)"**.
Como ya hemos explicado anteriormente también usamos **ngNativeValidate**, para decirle a Chrome que trate
las validaciones que definamos.
 
A cada campo input hay que definirle la el **ngModel y un **name**.
Si queremos referenciar la entrada con una variable en el componente.ts, escribimos **[ngModel]**.

             <input [ngModel]="email" name="email" class="form-control" type="email" required placeholder="Correo del usuario">
             <input ngModel name="password" class="form-control" type="password" required placeholder="Contraseña">
             <input [ngModel]="recuerdame" name="recuerdame" id="checkbox-signup" type="checkbox" class="filled-in chk-col-light-blue">

Si observamos las validaciones se están haciendo en el mismo html: **type="email" required**

Ejemplo del formaulario completo:
 
            <form ngNativeValidate #f="ngForm" class="form-horizontal form-material" (ngSubmit)="ingresar(f)" id="loginform" action="index.html">
                <a href="javascript:void(0)" class="text-center db"><img src="../assets/images/logo-icon.png" alt="Home" /><br/><img src="../assets/images/logo-text.png" alt="Home" /></a>
                <div class="form-group m-t-40">
                    <div class="col-xs-12">
                        <input [ngModel]="email" name="email" class="form-control" type="email" required placeholder="Correo del usuario">
                    </div>
                </div>
                <div class="form-group">
                    <div class="col-xs-12">
                        <input ngModel name="password" class="form-control" type="password" required placeholder="Contraseña">
                    </div>
                </div>
                <div class="form-group row">
                    <div class="col-md-12">
                        <div class="checkbox checkbox-primary pull-left p-t-0">
                            <input [ngModel]="recuerdame" name="recuerdame" id="checkbox-signup" type="checkbox" class="filled-in chk-col-light-blue">
                            <label for="checkbox-signup"> Recuérdame </label>
                        </div>
                        <a href="javascript:void(0)" id="to-recover" class="text-dark pull-right"><i class="fa fa-lock m-r-5"></i> Olvide contraseña?</a> </div>
                </div>
                <div class="form-group text-center m-t-20">
                    <div class="col-xs-12">
                        <button class="btn btn-info btn-lg btn-block text-uppercase btn-rounded" type="submit">Ingresar</button>
                    </div>
                </div>
                <div class="row">
                    <div class="col-xs-12 col-sm-12 col-md-12 m-t-10 text-center">
                        <div class="social">
                            <button type="button" id="btnGoogle" class="btn btn-googleplus" data-toggle="tooltip" title="Iniciar sesion con Google"> <i aria-hidden="true" class="fa fa-google-plus"></i> </button>
                        </div>
                    </div>
                </div>
                <div class="form-group m-b-0">
                    <div class="col-sm-12 text-center">
                        No tienes cuenta? <a routerLink="/register" class="text-primary m-l-5"><b>Crear cuenta</b></a>
                    </div>
                </div>
            </form>


### En el component.ts

Vamos a definir la funcion del submit

              ingresar(forma: NgForm) {
              
Si el formulario no es válido, salimos y no hacemos nada.

                if (forma.invalid) {
                  return;
                }
Si es valido, construimos a un usuario.

                const usuario = new Usuario(null, forma.value.email, forma.value.password);
                
Llamamos al servicio que va hacer que el usuario se logee, creando un token y nos subcribimos para que
se lance y cuando termine, nos navegue al dashboard de nuestra página.

                this._usuarioService.login(usuario, forma.value.recuerdame).subscribe( correcto => this.route.navigate(['/dashboard']));
              }
