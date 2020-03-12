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

### Mejores practicas en IAM

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
   
#### Eliminar las claves de acceso raíz

Esta marcada y de color verde lo que indica que esta tarea ya esta realizada o más bien no existen claves de acceso que borrar para **root** por que no se crearón automáticamente.

#### Activar MFA en la cuenta raíz

* **¿Qué es MFA?**
   * Acrónimo inglés para Multi-Factor Authentification
   * Capa adicional de seguridad para tu cuenta root
   * Código random de seis dígitos continuamente cambiante que necesitas poner (ademas de tu contraseña) para iniciar sesión en tu cuenta root.
   
* **¿Cómo consigo este código MFA?
   * Dispositivo virtual MFA
      * Teléfono o tableta
      * Aplicación de uso común (IOS y Android): Google Authenticator.
   * Dispositivo físico MFA(llavero físico)
      * Dispositivo físico pequeño con pantalla
      * Se compra directamente desde Amazon AWS





   























## Usuarios y politicas en IAM 07:33
## Grupos y politicas en IAM 07:13
## Roles en IAM 06:21
