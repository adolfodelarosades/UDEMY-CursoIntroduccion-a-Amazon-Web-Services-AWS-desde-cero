# 3. Identity & Access Management (IAM) 51:02

* ¿Qué es IAM? 06:50
* Configuración inicial de IAM 23:05
* Usuarios y politicas en IAM 07:33
* Grupos y politicas en IAM 07:13
* Roles en IAM 06:21

## ¿Qué es IAM? 06:50

En esta sección veremos la creación de IAM.

<img src="images/c3/3-iam.png">

Los temas que trataremos son:

* Que es IAM (Identity & Accesss Management )
* Configuración y parametrización de IAM
* Explicación de que es y para que se usan los: 
   * Usuarios
   * Grupos
   * Políticas
   * Roles
   
### Que es IAM

* Que es IAM
* Usos comunes en IAM
* La importancia de la cuenta root

#### Que es IAM

* IAM es donde administras tus usuarios de AWS y su acceso a sus cuentas y servicios de AWS.
* El uso común de IAM es administrar:
   * Usuarios
   * Grupos
   * Políticas de acceso de IAM
   * Roles
* Por defecto el **usuario root** tiene **acceso completo & total** a la cuenta.
* Por defecto cualquier usuario que cree en AWS se crea **sin acceso** a ningún servicio de AWS (excepto para poder iniciar sesión).
* Para todos los usuarios (excepto usuario root) se deben otorgar permisos que permitan el acceso a los servicios de AWS.
* La opción IAM la tenemos en el Grupo **Seguridad, identidad y conformidad** 

   <img src="images/c3/3-iam-2.png">

   Si entramos a la opción IAM tenemos:
   
   <img src="images/c3/3-iam-3.png">
   
   [Video](https://www.youtube.com/watch?time_continue=135&v=Ul6FW4UANGc&feature=emb_logo)

Cuando creamos la cuenta AWS, a su vez se creo el usuario **root** basado en los datos inroducidos como email, nombre, etc. 

#### Usos comunes en IAM

El uso común de IAM es administrar todos los Grupos, Usuarios, Roles, Políticas

#### La importancia de la cuenta root

El usuario **root** tiene acceso a todos los servicios y configuraciones de AWS.

Cuando creamos un nuevo usuario con IAM este se crea sin ningún acceso de los servicios de AWS, lo único que pueden hacer es iniciar sesión. Para que tenga acceso a los servicios de AWS nos apoyaremos con los Grupos, Usuarios, Roles y Políticas de acceso.

## Configuración inicial de IAM 23:05

Los temas que trataremos son:

* Mejores practicas en IAM
* MFA en IAM
* Creación de un usuario y grupo administrador
* Creación de políticas de password en IAM

### Mejores Practicas en IAM

* Pautas que recomiendan configuraciones de arquitectura con el propósito de alcanzar un nivel alto en seguridad, accesibilidad y eficiencia.

* Cuando se crea una nueva cuenta root en AWS, es muy buena práctica completar las tareas enumeradas en la sección de "Estado de seguridad" en IAM. Si entramos a IAM veremos a lo que nos referimos:

<img src="images/c3/3-iam-3.png">

Para cumplir con las Mejores practicas de IAM debemos cumplir con las siguientes tareas:

* Estas tareas incluyen lo siguiente:
   * Eliminar las claves de acceso raíz
   * Activar MFA en la cuenta raíz
   * Crear usuarios de IAM individuales
   * Utilizar grupos para asignar permisos
   * Aplicar una política de contraseñas de IAM
   
#### Eliminar las Claves de Acceso Raíz

Esta marcada y de color verde lo que indica que esta tarea ya esta realizada o más bien no existen claves de acceso que borrar para **root** por que no se crearón automáticamente.

#### Activar MFA en la Cuenta Root

* **¿Qué es MFA?**
   * Acrónimo inglés para Multi-Factor Authentification
   * Capa adicional de seguridad para tu cuenta root
   * Código random de seis dígitos continuamente cambiante que necesitas poner (ademas de tu contraseña) para iniciar sesión en tu cuenta root.
   
* **¿Cómo consigo este código MFA?**
   * Dispositivo virtual MFA
      * Teléfono o tableta
      * Aplicación Google Authenticator de uso común (IOS y Android). Instalar Google Authenticator.
   * Dispositivo físico MFA(llavero físico)
      * Dispositivo físico pequeño con pantalla
      * Se compra directamente desde Amazon AWS

Arquitectura de MFA.

<img src="images/c3/3-mfa-1.png">

Cuando activemos MFA en la cuenta **root**, lo que estamos haciendo es añadiendo un paso intermedio al inicio de sesión del usuario **root**, una vez que ingresemos el email y password se nos solicitará el código MFA, el cual lo encontraremos en el móvil, en la aplicación Google Authenticator, una vez que ingresemos dicho código MFA se nos permitirá entrar a la cuenta de **root**.

Vamos a ver como se activa MFA, pulsamos en **Activar MFA en la cuenta raíz**.

<img src="images/c3/3-mfa-2.png">

Presionamos el botón **Administrar MFA**, nos lleva a la siguiente pantalla, donde debemos seleccionar la segunda opción **Multi-Factor Authentication (MFA)**.

<img src="images/c3/3-mfa-3.png">

Aquí pulsaremos el botón **Activar MFA**, nos presenta el siguiente PopUp:
 
<img src="images/c3/3-mfa-4.png">

Seleccionamos la opción **Dispositivo MFA virtual**, al presionar el botón **Continuar**

<img src="images/c3/3-mfa-5.png">

Aquí se nos presenta un código Bidi el cual debemos escanear con el móvil con la aplicación Google Authenticator. En la aplicación móvil nos apareceran los códigos de MFA1 y MFA2. Los introducimos y presionamos en **Asignar MFA**.

Finalmente se nos indica que **hemos asignado un tipo de MFA virtual correctamente**.

<img src="images/c3/3-mfa-6.png">

Al entrar en IAM ya vemos que la opción **Activar MFA en la cuenta raíz** esta activa.

<img src="images/c3/3-mfa-7.png">

*A partir de aquí, cada que nos conectemos como root se nos pedirán los códigos MFA*

#### Crear Usuarios de IAM Individuales

* Mejor practica en IAM es **NUNCA** usar la cuenta root para el día a día

* Si quieres tener acceso de administrador completo, crea un usuario de IAM y adjunta la política de "AdministratorAccess" al usuario.

* Luego usa esta nueva cuenta con acceso de administrador diariamente.

Vamos a crear usuario, pulsamos en **Crear usuarios de IAM individuales**.

<img src="images/c3/3-usuario-1.png">

Vamos a presionar el botón **Administrar los usuarios**. Nos llevara a la sección de Usuarios y por el momento no tenemos ninguno.

<img src="images/c3/3-usuario-2.png">

Vamos a presionar sobre el botón **Añadir usuario(s)**.

<img src="images/c3/3-usuario-3.png">

Se nos iran presentando diferentes pantallas que tenemos que rellenar:

<img src="images/c3/3-usuario-4.png">

Presionamos **Siguiente: Permisos**

<img src="images/c3/3-usuario-5.png">

Presionamos **Siguiente: Etiquetas**

<img src="images/c3/3-usuario-6.png">

Presionamos **Siguiente: Revisar**

<img src="images/c3/3-usuario-7.png">

Presionamos el botón **Crear un usuario**

<img src="images/c3/3-usuario-8.png">

Se nos indica que el usuario ha sido creado. Presionamos **Cerrar**

<img src="images/c3/3-usuario-9.png">

Como podemos observar al regresar al Panel de Usuarios ya tenemos el usuario **Jose** que acabamos de crear. 

Si regresamos al Paner de IAM la opción **Crear usuarios de IAM individuales** ya la tenemos marcarcada como hecha. Ademas tenemos **Usuarios: 1** que nos indica que tenemos un usuario.

<img src="images/c3/3-usuario-10.png">

*Con esto ya podemos Iniciar Sesión con el usuario Jose en lugar de root, teniendo acceso como Administrador para realizar cualquier cambio que necesitemos*.

#### Utilizar Grupos para Asignar Permisos

* A menudo puede ser más conveniente y eficiente configurar grupos y asignar permisos al grupo en lugar de administrar a cada usuario individualmente.

Vamos a utilizar grupos para asignar permisos, pulsamos en **Utilizar grupos para asignar permisos** y presionamos el botón **Administrar los grupos**.

<img src="images/c3/3-grupos-1.png">

Presionamos el botón **Crear un grupo**.

<img src="images/c3/3-grupos-2.png">

Introducimos el nombre `Admin_JMG` y presionamos el botón **Paso siguiente**.

<img src="images/c3/3-grupos-3.png">

Aquí podemos asociar todas las políticas necesarias al grupo, en este caso solo seleccionamos `AdministratorAccess` y pulsamos el botón **Paso siguiente**.

<img src="images/c3/3-grupos-4.png">

Finalmente pulsamos en **Crear un grupo**.

<img src="images/c3/3-grupos-5.png">

Como podemos ver ya tenemos creado el grupo Admin_JMG que tiene asignada la política `AdministratorAccess`, pero aun no tiene ningun usuario asignado. Si regresamos al panel de IAM, veremos que ya tenemos marcada la opción de **Utilizar grupos para asignar permisos**.

#### Aplicar una Política de Contraseñas de IAM

* Una política de contraseñas dicta las reglas de formato y caducidad que se deben seguir cuando un usuario crea o modifica su contraseña.

* Estas reglas incluyen lo siguiente:
   * Longitud
   * Si son Case Sensitive
   * Si requieren Números
   * Si requieren caracteres No-AlfaNumericos
   * Si el password expira
   * Si el password se puede reusar.
   
Vamos a aplicar una política de contraseñas   , pulsamos en **Aplicar una Política de Contraseñas de IAM** 

<img src="images/c3/3-pol-1.png">

y presionamos el botón **Administrar la política de contraseñas**.

<img src="images/c3/3-pol-2.png">

Presionamos el botón **Establecer la política de contraseñas**

<img src="images/c3/3-pol-3.png">

Presionamos el botón **Guardar los cambios**

<img src="images/c3/3-pol-4.png">

Se nos indica que **Se actualizó la política de contraseñas**. 

Si regresamos al panel IAM vemos que ya tenemos marcada la opción de **Aplicar una Política de Contraseñas de IAM**

<img src="images/c3/3-pol-5.png">

Por lo que ya hemos cumplido con todas las tareas dentro de IAM en cuanto a la configuración inicial de IAM.

## Usuarios y Políticas en IAM 07:33

* Crear, usar y gestionar usuarios en IAM
* Entender las políticas de IAM
* Como se aplican las políticas a los usuarios

Imaginemos que tenemos el siguiente escenario:

<img src="images/c3/3-escenario.png">

Tenemos nuestra cuenta de AWS, tenemos configurado IAM, dentro de IAM tenemos un usuario llamado Jose, y tenemos el servicio S3 de AWS. Jose necesita acceder a S3 para almacenar archivos. 

En este preciso momento con lo que tenemos configurado Jose no tiene acceso a S3.

<img src="images/c3/3-escenario-2.png">

Para eso nos serviran las políticas de acceso.

<img src="images/c3/3-escenario-3.png">

en partícular a Jsose le debemos aplicar la **política Full Access de S3** para que pueda tener acceso a S3.

Para hacer esto en la consola nos vamos primero al panel de Usuarios en AWS.

<img src="images/c3/3-escenario-4.png">

Presionamos el usuario Jose.

<img src="images/c3/3-escenario-5.png">

Como podemos observar tenemos varias pestañas **Permisos Grupos Etiquetas** etc. Aquí nos va a interesar es la pestaña de **Permisos** la cual por el momento tiene asociada la poítica de `AdministratorAccess`, vamos a presionar el botón **Añadir permisos**.

<img src="images/c3/3-escenario-6.png">

Vamos a seleccionar **Asociar directamente las políticas existentes** en el buscador ponemos **S3** y seleccionamos **AmazonS3FullAccesss** y presionamos en **Siguiente: Revisar**.

<img src="images/c3/3-escenario-7.png">

Presionamos **Añadir permisos**.

<img src="images/c3/3-escenario-8.png">

como vemos Jose ya tiene permiso para S3.

Es posible que tuvieramos mas usuarios en IAM pero que no tuvieran acceso a S3.

<img src="images/c3/3-escenario-9.png">

Vamos al panel de Usuarios para añadir los usuarios Miguel y David. 

<img src="images/c3/3-escenario-10.png">

Presionamos el botón **Añadir usuario(s)**.

<img src="images/c3/3-escenario-11.png">

Introducimos los dos usuarios que queremos crear y su password. Presionamos el botón **Siguiente: permisos**.

Actualmente Miguel y David no tendran acceso a S3.

<img src="images/c3/3-escenario-12.png">

Por lo que vamos a dar en **Asociar directamente las políticas existentes** y buscamos S3, para seleccionar **AmazonS3FullAccess** 

<img src="images/c3/3-escenario-13.png">

Presionamos **Siguiente: etiqueta**.

<img src="images/c3/3-escenario-14.png">

Presionamos **Siguiente: revisar**.

<img src="images/c3/3-escenario-15.png">

Presinamos en el botón **Crear usuarios**.

<img src="images/c3/3-escenario-16.png">

Precionamos en **Cerrar**

<img src="images/c3/3-escenario-17.png">

Como vemos ya tenemos nuestros 3 usuarios Jose, Miguel y David y los 3 tienen la politica adjuntada de Full Access S3 por lo que podrán tener acceso a S3.

<img src="images/c3/3-escenario-18.png">

**Unimos las políticas a los usuarios para permitir el acceso a los recursos de AWS.**

## Grupos y Políticas en IAM 07:13

* Crear, usar y gestionar grupos en IAM.
* Como se aplican las políticas a los grupos.

Hasta el momento hemos creado tres usuarios y a cada uno de ellos le hemos dado acceso a S3 de manera individual, es decir asignando la política de acceso a S3 a cada uno de los usuarios, pero esta manera de gestionar los permisos no es la más adecuada, ya que si crece el numero de usuarios, debemos asignar las políticas de acceso a cada uno de ellos complicandose la gestión.

Recordemos que uno de los usos comunes de IAM ademas de administrar Usuarios y Políticas también administra Grupos. 

Por lo que vamos a eliminar la política `AmazonS3FullAccess` de cada uno de los usuarios.

Entramos al panel de Usuarios.

<img src="images/c3/3-escenario-17.png">

Entramos en el usuario Jose.

<img src="images/c3/3-escenario-19.png">

Eliminamos la política `AmazonS3FullAccess` pulsando en la X, nos aparece un PopUp.

<img src="images/c3/3-escenario-20.png">

Pulsamos en **Desasociar**.

<img src="images/c3/3-escenario-21.png">

Podemos ver que ya elimino la política asociada `AmazonS3FullAccess`, repetimos lo mismo para los usuarios David y Miguel.

Por lo que ahora mis tres usuarios Miguel, Jose y David ya no tienen acceso a S3.

<img src="images/c3/3-escenario-22.png">

Lo que vamos a hacer ahora es crear un **Grupo Desarrollo** 

<img src="images/c3/3-escenario-23.png">

Por lo que nos vamos a la consola en la sección de Grupos

<img src="images/c3/3-escenario-24.png">

Pulsamos en el botón **Crear un grupo**.

<img src="images/c3/3-escenario-25.png">

Metemos de nombre **Desarrollo** y pulsamos en el botón **Paso siguiente**.

<img src="images/c3/3-escenario-26.png">

Aquí aun no vamos a meter ninguna política por lo que presionamos **Paso siguiente**.

<img src="images/c3/3-escenario-27.png">

Presionamos botón **Crear un grupo**.

<img src="images/c3/3-escenario-28.png">

Ya tenemos un grupo vacío sin ningún usuario y sin ninguna política de acceso a ningún recurso de AWS.

Lo siguiente que vamos a hacer es asignar los usuarios Miguel, Jose y David al grupo Desarrollo.

<img src="images/c3/3-escenario-29.png">

Por lo que seleccionamos el Grupo Desarrollo.

<img src="images/c3/3-escenario-30.png">

Presionamos el botón **Añadir usuarios al grupo**

<img src="images/c3/3-escenario-31.png">

Seleccionamos los usuarios David, Jose y Miguel y presionamos el botón **Añadir usuarios**

<img src="images/c3/3-escenario-32.png">

Con esto ya tenemos incluidos a los usuarios en el Grupo Desarrollo. Pero hasta el momento el Grupo Desarrollo no tiene acceso a S3.

<img src="images/c3/3-escenario-33.png">

Lo que vamos a hacer es asignarle la política `AmazonS3FullAccess` al grupo y esto implicitamente dara acceso a todos los usuarios que pertenezcan al grupo a S3.

Por lo que vamos a la pestaña **Permisos** en la sección **Grupos**.

<img src="images/c3/3-escenario-35.png">

Pulsamos **Asociar la política**.

<img src="images/c3/3-escenario-36.png">

Buscamos S3 y seleccionamos **AmazonS3FullAccess** y presionamos el botón **Asociar la política**

<img src="images/c3/3-escenario-37.png">

De esta manera hemos asociado la política `AmazonS3FullAccess` a nuestro Grupo Desarrollo.

<img src="images/c3/3-escenario-34.png">

Con esto hemos logrado dar acceso a S3 a todos los usuarios que pertenecen al Grupo Desarrollo, teniendo la gran ventaja de que no fue necesario asociar la política a cada uno de los usuarios, basto hacerlo al grupo a cual pertenecian, es decir asociamos la política una sola vez en vez de 3, si fueran 10 o más usuarios se ven las ventajas se haria solo una vez.

Si borramos el usuario Jose del Grupo Desarrollo, Jose piede el acceso a S3.

<img src="images/c3/3-escenario-38.png">

Vamos a borrarlo. Vamos a la pestaña **Usuarios** de la sección Grupo.

<img src="images/c3/3-escenario-39.png">

Seleccionamos **Eliminar al usuario del grupo** para Jose.

<img src="images/c3/3-escenario-40.png">

Nos sale un PopUp para confirmar la eliminación, pulsamos en **Quitar del grupo**.

<img src="images/c3/3-escenario-41.png">

Con esto tenemos que como Jose ya no pertenece al Grupo Desarrollo y por consecuencia a dejado de tener acceso a S3.

<img src="images/c3/3-escenario-42.png">

Para que Jose vuelva a tener acceso a S3 tenemos dos opciones.

* Asociar la política de acceso a Jose.
* Incluir a Jose en el grupo nuevamente.

Incluyamos a Jose nuevamente al grupo.

<img src="images/c3/3-escenario-43.png">

Con lo que el esquema final que tenemos es el siguiente:

<img src="images/c3/3-escenario-44.png">

## Roles en IAM 06:21

* Crear, usar y gestionar roles en IAM
* Entender como se aplican y se usan los roles

### Crear, usar y gestionar roles en IAM

Partiendo del último esquema, imaginemos que tenemos una instancia, una maquina virtual EC2 la cual quiere acceder al almacenamiento S3 en mi AWS. Es decir que tenemos un servicio de AWS(EC2) que quiere comunicarse con otro servicio de AWS(S3).

<img src="images/c3/3-rol-1.png">

Podriamos pensar que para que EC2 tenga acceso a S3 bastaría con agregar a EC2 la política de acceso `AmazonS3FullAccess`, pero EC2 no es un Usuario ni un Grupo es un Servicio de AWS por lo que esta opción no es correcta.

<img src="images/c3/3-rol-2.png">

En AWS **NO** podemos adjuntar políticas directamente a otros servicios de AWS. Con lo que en vez de adjuntar una política a un servicio de AWS lo que necesitamos adjutar es un **ROL**.

<img src="images/c3/3-rol-3.png">

Una vez que adjuntemos un Rol IAM al servicio de instancias de Amazon(EC2) nos dara permisos para acceder al servicio S3.

**Lo que hace reamente un Rol es dar permisos a un servicio para que pueda interactar con otro servicio.**

En el panel IAM seleccionamos la sección **Roles**

<img src="images/c3/3-rol-4.png">

Presionamos el botón **Crear un rol**.

<img src="images/c3/3-rol-5.png">

Vemos todos los diferentes roles que podemos asignar a los distintos servicios de AWS. En este caso seleccionamos EC2 y presionamos en **Siguiente: Permisos**.

<img src="images/c3/3-rol-6.png">

Vamos a asignar a este Rol la política `AmazonS3FullAccess`, con lo que podemos pensar que un rol, es casi como un grupo que asignamos a servicios en lugar de asignarlo a usuarios. Presionamos **Siguiente: Etiquetas**.

<img src="images/c3/3-rol-7.png">

Presionamos **Siguiente: Revisar**.

<img src="images/c3/3-rol-8.png">

Damos el nombre de rol **Role_Desarrollo** y presionamos el botón **Crear un rol**.

<img src="images/c3/3-rol-9.png">

Con esto vemos que hemos creado el rol **Role_Desarrollo**, el cual va a permitir que el servicio de EC2, de maquina virtual, pueda interactuar con otro servicio en este caso S3. 

### Asignación de 2 nuevas Políticas al Grupo de Desarrollo

Vamos a la sección de **Groups** en la pestaña **Permisos**

<img src="images/c3/3-poli-1.png">

Presionamos en **Asociar la política**.

Buscamos `AmazonEC2FullAccess` y la marcamos.

<img src="images/c3/3-poli-2.png">

Buscamos `AmazonRDSFullAccess` y la marcamos.

<img src="images/c3/3-poli-3.png">

Presionamos en **Asociar la política**.

<img src="images/c3/3-poli-4.png">

Con lo cual ya tenemos en el Grupo de Desarrollo con las políticas `AmazonS3FullAccess`, `AmazonEC2FullAccess` (Maquinas Virtuales) y `AmazonRDSFullAccess` (Acceso a BD), las cuales nos serviran en futuras lecciones.

