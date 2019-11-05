# Formularios en Angular

En Angular podemos implementar dos tipos de formulario: **Por Template y Reaktiv Form**.

## Reaktiv form

### En el hmtl:

Hay que decile a Angular que ese formulario va ser tratado como un Reaktivform.

Le definimos el formGroup que será una referencia al formulario y tratamos el Submit,
en vez de dejarlo en un botón con type="submit".

            <form [formGroup]="forma" (ngSubmit)="registrarUsuario()"

A cada entada hay que definirle un **formControlName** y un **name**.

            <input formControlName="nombre" name="nombre" class="form-control" type="text" required placeholder="Nombre">
            <input formControlName="correo" name="correo" class="form-control" type="text" required placeholder="Correo">
            <input formControlName="password" name="password" class="form-control" type="password" required placeholder="Contraseña">
            <input formControlName="password2" name="password2" class="form-control" type="password" required placeholder="Confirmar contraseña">
            
Al haber definido el submit en la etiqueta del form, le estamos diciendo a Angular que trate a este
formulario como un Reaktivform y cuando se encuentre otro submit en algún botón, lova a ignorar.

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
