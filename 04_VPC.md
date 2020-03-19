# 4. Virtual Private Cloud (VPC) 01:39:57

* Infraestructura Global en AWS 10:13
* Introducción a VPC 13:14
* Internet Gateways (IGW) 07:43
* Tablas de rutas (RTs) 10:32
* Network Access Control List (NACLs) 23:09
* Subredes 15:18
* Availability Zones (AZs) 19:48

## Infraestructura Global en AWS 10:13

* Regiones
* Availability Zones (AZs)
* Data Centers

En esta sección vamos a profundizar bastante en el componente estrella de Amazon, que es donde esta la mayoría de la funcionalidad de AWS, porsupuesto hablamos de VPC. 

Hasta el momento hemos construído esto:

<img src="images/c4/4-0.png">

En esta sección construiremos lo siguiente:

<img src="images/c4/4-1.png">


### Regiones

¿Qué son las regiones de AWS?

* Agrupación de recursos de AWS ubicados en una zona geográfica.
* Diseñado para dar servicio a clientes de diferentes regiones.
* Las regiones forman parte de múltiples zonas de disponibilidad.

<img src="images/c4/4-1-2.png">

Algo muy importante que mencionar ahora es que la infraestructura global de Amazon empieza por las regiones y las regiones son agrupaciones de recursos de AWS ubicados en una zona geográfica en concreto.

Con lo que si le echas un vistazo a este mapa de Amazon, los circulitos de color naranja que ves son regiones de Amazon y los de color blanco son regiones que se están desplegando o instalando en la actualidad. 

Con lo que estas regiones han sido diseñadas para dar servicio a clientes de diferentes regiones.

Resumiendo las regiones son zonas geográficas donde Amazon provee servicio a sus clientes con lo que si resides en Europa por ejemplo en Irlanda y quieres usar los servicios de Amazon estás de enhorabuena porque Amazon tiene una región con tres centros de datos en Dublín.

Y digo que estoy de suerte y enhorabuena porque si quisiera poner mis instancias o mis servicios en la zona de Dublín, al tener centro de datos Amazon en Dublín la latencia de mi servicio para los clientes de Dublín sería muy pequeña ya que físicamente el centro de datos de Amazon donde voy a albergar mis servicios de Amazon está físicamente en Dublín. 

Con lo que te estarás preguntando que muy bien estás enhorabuena porque resido en Dublín.

Pero qué pasa para mis clientes que están en Tokio y quieren conectarse al servidor web que voy a poner en la zona geográfica de Dublín.

Pues muy buena pregunta, durante el transcurso de este curso veremos cómo crear el mismo servidor web que tengo en Dublín, también en la zona geográfica de Asia, para que los clientes de Japón que se conecten a mi servidor web se conecten directamente al servicio, al servidor web que tendré replicado en la zona de Japón para que obviamente los usuarios de Japón tengan también una latencia muy pequeña.

Otra cosa muy importante a destacar en este gráfico es que cada región está compuesta por diferentes zonas de disponibilidad y el número denota cuántas zonas de disponibilidad tenemos disponibles por cada región en Amazon. 

Con lo que te estarás preguntando qué es una zona de disponibilidad en AWS.

### Availability Zones (AZs)

¿Qué son las Availability Zones (AZs) en AWS?

* Zonas geográficamente aisladas dentro de una región que alberga recursos AWS.
* Las zonas disponibles son lugares donde se encuentran los centros de datos físicos de AWS.
* Múltiples AZs en cada región proporcionan redundancia para los recursos de AWS en esta región.

<img src="images/c4/4-1-3.png">

Pues bien estas Availability Zones (zonas de disponibilidad) son realmente zonas geográficamente aisladas dentro de una misma región que albergan recursos de AWS, con lo que realmente estas zonas de disponibilidad son lugares físicos donde se encuentran los centros de datos de AWS.

Pero lo más importante de estas AZs, es que múltiples AZs en cada región nos proporcionarán redundancia para los recursos de AWS que pongamos en esa región.

¿Qué significa esto?

En el mapa verás que por ejemplo en la zona de América Latina concretamente en Brasil, tenemos una región de Amazon con un número 3.

Esto significa que tenemos tres centros físicos de Amazon o tres AZs, en otras zonas geográficas tenemos dos y en otras hasta cuatro, pero mínima deberíamos de tener al menos dos AZs por región.

Con lo que entiende que por cada región al menos tendremos dos AZs o dos centros de datos físicamente aislados uno del otro, para proporcionarnos redundancia y alta disponibilidad para nuestros servicios de AWS.

Esto es tremendamente importante y quizás aquí radica el éxito de las soluciones de Amazon. 

Si seguimos el ejemplo de S3 el servicio de almacenamiento de objetos en Amazon y ponemos por ejemplo un archivo en una zona de disponibilidad dentro de la región de Dublín, que como sabes Dublín tiene tres AZs diferentes, es decir tres centros de datos físicos conectados el uno con el otro. 

Pues imagínate que una de las AZs se cae porque ha habido un huracán o un incendio o se ha caído el centro de datos. En ese caso no tendríamos ningún problema, porque los archivos de S3 se replican dentro de una misma región en las tres zonas diferentes, con lo cual cualquier zona de disponibilidad que se caiga, no habría ningún problema, porque los archivos han sido replicados como digo en otras de las zonas de disponibilidad de la misma región, con lo que el tener diferentes zonas de disponibilidad, nos proporciona redundancia para los servicios que vayamos a instalar en AWS.

Con lo que en resumen las zonas de disponibilidad, nos proporciona la arquitectura en alta disponibilidad para todos los servicios que vayamos a poner en AWS.

### Data Centers

Los Data Centers es donde se encuentra el hardware físico que ejecuta los servicios de AWS.

<img src="images/c4/4-1-4.png">

Y si entramos en cada Availability Zones o zona de disponibilidad, es donde encontraremos ya el centro de datos físico que tiene Amazon, que es realmente donde tenemos físicamente los servidores que almacenan los servicios en Amazon AWS. 

Son todos los servidores los switches de red, el almacenamiento, toda la circuitería se encuentran en un centro físico de Amazon. 

Y si bajamos más de nivel y entramos físicamente al centro de datos de Amazon nos encontramos con todos los servicios disponibles que vamos a crear en estos centros de datos totalmente redundados de Amazon AWS.

<img src="images/c4/4-1-5.png">

Con lo que todos los servicios que vamos a ir instalando, los balanceadores, internet gategay, los usuarios(IAM), los archivos en S3, las instancias EC2, las base de datos RDS que vamos a ir creando, etc. reside obviamente en un centro de datos físico.

Es decir todo lo que vamos a crear desde la GUI, desde la consola de Amazon, residiera obviamente en algunos de los centro de datos o zonas disponibles que Amazon tiene disponibles por todo el mundo y que obviamente estos centros de datos estarán disponibles en una zona de disponibilidad y esas zonas de disponibilidad están disponibles en las regiones de AWS.

Si estoy en la región de Irlanda, donde tengo 3 AZs o tres centros de datos diferentes para dotar de alta disponibilidad a los servicios que vaya a albergar en esta zona de disponibilidad, con lo que cuando vaya a crear nuevos servicios en la zona de Irlanda, esos servicios van a quedar albergados en esta región de Europa, que a su vez se crearán en alguna de las tres zonas de disponibilidad que tiene la región de Irlanda y que a su vez se crearán en un centro de datos físicos.

Con esto terminamos este amplio resumen a los servicios de infraestructura de AWS.

## Introducción a VPC 13:14

* Definición de las VPCs
* Discución conceptual de las VPCs
* Componentes en las VPCs
* Flujo de datos dentro de las VPCs
* Acceso a las VPCs desde la consola AWS

### Acceso a las VPCs desde la consola AWS

Para acceder a las VPC en la consola de Amazon la encontramos en la Sección **Redes y entrega de Contenido**

<img src="images/c4/4-1-6.png">

Si damos click en VPC veremos el VPC Dashboard:

<img src="images/c4/4-1-7.png">

### Definición de las VPCs

* ¿Qué es una VPC (Virtual Private Cloud) JMG
   
   * Es una subsección privada de AWS que **TU** controlas y en la que puedes meter los recursos de AWS como instancias EC2 y BD.
   * Tu tienes el control TOTAL sobre quien tiene acceso a los recursos de AWS que vas a instalar dentro de tu VPC.
   
* ¿Qué es una VPC según AWS?

   * La nube privada virtual de Amazon te permite aprovisionar una sección aislada de la nube de Amazon Web Services (AWS) donde puedes iniciar recursos en una red virtual que tu defines.
   * Tendrás control total sobre tu entorno de red virtual, incluyendo la sección de tu propio rango de direcciones IP, la creación de subredes y configuración de tablas de rutas y puertas de enlace de red.
   
**Cuando creas una cuenta AWS, se crea una VPC por defecto**

Por lo que en nuestro VPC Dashboard vemos que ya tenemos un VPC, también vemos que se han creado 3 Subnets, se ha creado 1 Route Tables, 1 Network ACLs, 1 Security Groups, 1 Internet Gateways y 1 DHCP options sets.

AWS crea todo esto para que podamos tener una VPC completamente funcional para poder desplegar instancias y que todo funcione correctamente y **totalmente Gratuita**.

### Discución conceptual de las VPCs

Para entender que es una VPC podemos pensar que es muy similar a la red de nuestra casa.

<img src="images/c4/4-1-8.png">

En la red de nuestra casa tenemos cables que vienen de Internet/ISP los cuales se conectan al Router, es posible que tengamos instalado un Firewall para evitar que entre trafico no deseado antes de conectar todos nuestros dispositivos a Internet.

¿Qué pasa si se cae el cable que se conecta desde el Router con el proveedor de Internet?

<img src="images/c4/4-1-9.png">

Ninguno de los dispositivos conectados en nuestra red privada en casa podría salir a Internet, pero las maquinas entre si podrían hablar perfectamente ya que estan conectadas a través del Router y la conexión con el Router esta funcionando perfectamente.

¿Qué pasa si lo que se cae es el Router?

<img src="images/c4/4-1-10.png">   

Que todos los dispositivos conectados al Router no podrían conectarse entre ellos. 

Como ves son posibles escenarios que pueden pasar en tu red virtual en casa muy parecido a lo que es una VPC.


### Componentes en las VPCs

Si te das cuenta los componentes de una VPN son muy similares a los componentes que te he mostrado de tu red privada en casa, tenemos el acceso a Internet el cual se conecta con un **Internet Gateway**, en la conexión de tu casa es el **cable DSL o de fibra**.

<img src="images/c4/4-1-11.png"> 

En seguida tenemos **tablas de rutas** que equivale al router en la red privada en casa.

Después de estas tablas de rutas tenemos en Amazon **Network Access Control List (NACL)** que sería muy similar al **Firewall** que puedes tener en tu red privada en casa.

Y en lugar de tener **PCs o teléfonos inteligentes smartphones** lo que tenemos en nuestra VPC son **instancias de EC2 o máquinas virtuales**.

He querido hacer esta comparación para que no te asustes cuando vayamos a hacer los laboratorios o expliquemos el concepto de la VPC porque realmente estamos hablando de Internet Gateways, de tablas de rutas, de Network Access Control Listy de instancias.

Haciendo esta comparación con tu red privada en casa tendrás más fácil la posibilidad de entender cómo administrar, instalar y gestionar una VPC y todos los componentes dentro de esa VPC en AWS.

### Flujo de datos dentro de las VPCs

Así que el flujo de datos que va a ocurrir en una VPC es muy parecido al flujo de datos que tendrás también en tu red privada en casa.

Es decir si en el EC2 tenemos una instancia la cual quieres salir a Internet para ver una página web esta petición va a pasar por el Network Access Control List que va a decir si este protocolo está abierto o no si está abierto va a pasar a nuestra tabla de rutas que sería como el router que tienes en tu casa y este router se lo va a pasar al Internet Gateway que sería como el cable de ADSL o de fibra que te conecta en la red privade de casa y este conecta con tu proveedor de Internet.

Así que el flujo de datos en una VPC es casi exactamente igual que el flujo de datos que puedas tener desde un dispositivo móvil o un PC portátil en una red privada de tu casa.

**Recuerda**

* ¿Qué es una VPC?

   * La nube privada virtual de amazon te permite aprovisionar una sección aislada de la nube de Amazon Web Services (AWS) donde puedes iniciar recursos de AWS en una red virtual que tu defines.
   * Tendrás control total sobre tu entorno de red virtual, incluyendo la sección dee tu propio rango de direcciones IP, la creación de subredes y configuración de tablas de rutas y puertas de enlace de red.

* Cuando creas una cuenta en AWS, se crea una VPC por defectocon los siguientes componentes que se necesitan para hacerla funcionar:

   1. Internet Gateway (GW).
   2. Una tabla de rutas(con rutas a las subredes por defecto).
   3. Un NACL (con reglas predefinidas para garantizar acceso).
   4. Subredes para provisionar recursos AWS(instancias EC2).
   
## Internet Gateways (IGW) 07:43

## Tablas de rutas (RTs) 10:32

## Network Access Control List (NACLs) 23:09

## Subredes 15:18

## Availability Zones (AZs) 19:48

