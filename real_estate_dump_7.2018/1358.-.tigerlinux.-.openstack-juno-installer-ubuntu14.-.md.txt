# Instalador Desatendido (Semi Automatizado) para OpenStack (JUNO)
Reynaldo R. Martinez P.
E-Mail: TigerLinux@Gmail.com
Caracas, Venezuela.

## Introducción

Este instalador fue realizado para automatizar las tareas de creación de una
infraestructura de virtualización basada en OpenStack. Hasta el momento,
existen tres "sabores" del instalador, uno para Debian 7, uno para Centos 7,
y finalmente uno para Ubuntu 14.04 LTS.

Las tres versiones producen un OpenStack utilizable en producción, pero recomen-
damos en el caso de Centos 7 esperar a que el sistema operativo madure lo sufi-
ciente antes de considerarlo realmente listo para producción.

En resumen, este instalador puede producir un OpenStack Juno completamente
utilizable en ambientes de producción, sin embargo, recuerde que el factor "bugs"
no depende de nosotros, sino del proyecto OpenStack y de los proyectos que 
empaquetan para centos, debian y ubuntu.

También tome en cuenta que "hasta la fecha" (y eso podría cambiar en el futuro)
los paquetes de Centos (provistos por el proyecto RDO de RedHat) tienden a
actualizarse mas a menudo que los paquetes para Debian 7 en "gplhost".

Los paquetes de Ubuntu son los que normalemte están mas actualizados.

## Uso del Instalador.

### Primero

*LEA, LEA, LEA y luego de descansar de leer, LEA DE NUEVO !!.*

Lea todo lo que pueda de *OpenStack* si desea incursionar en el área de
virtualización en la nube.  Si no le gusta leer, entonces apóyese en alguien
que si tenga la disposición para hacerlo, pero no trate de usar este
instalador sin tener algún tipo de conocimientos a la mano. Vea el archivo
`NOTAS.txt` para entender un poco mas de cuales conocimientos usted debería
tener.

El sub-mundo de *OpenStack* engloba varias tecnologías del mundo de Software
Libre y del mundo de Redes que deben ser comprendidas muy bien antes de
siquiera intentar hacer cualquier instalación de openstack ya sea con esta
herramienta de instalación o con cualquier otra. En resumen, si usted no tiene
los conocimientos, no lo intente. Adquiera los conocimientos primero, y luego
proceda !.

Antes de usar el instalador, debe preparar su o sus servidores. De nuevo, en
el archivo `NOTAS.txt` hay puntos importantes que deben ser cubiertos antes de
iniciar una instalación usando estas herramientas. El instalador hará una
serie de validaciones que, en caso de arrojar resultados negativos, hará que
aborte el proceso.

### Segundo: Modifique el archivo de configuración del instalador.

El instalador tiene un archivo central de configuración:
`./configs/main-config.rc`. Dicho archivo está bastante documentado, de manera
que si usted hizo *su tarea* y estudió de *OpenStack*, sabrá que debe modificar
en el mismo. Hay cosas muy obvias como *contraseñas*, *direcciones IP*,
*módulos a instalar* y *dominios de dns*.

En su versión por defecto, el archivo de configuración tiene las selecciones
de módulos para instalar lo que se conoce como un "all-in-one" (un servidor
monolítico de *OpenStack* con todos los servicios mas usados).

Adicionalmente, existen tres módulos que por defecto están en "no":
*Heat*, *Swift*, *Trove*, *Sahara* y *SNMP*. El módulo de swift se puede instalar
"si usted realmente va a usarlo". *Swift* por si solo ya es casi tan extenso como
todo *OpenStack*. Úselo si **REALMENTE** sabe lo que está haciendo y si **REALMENTE**
lo va a utilizar. El módulo de *SNMP* instala variables de monitoreo útiles si
usted va a monitorear *OpenStack* vía *SNMP* pero no instala ningún tipo de
aplicación de monitoreo. Las variables están descritas (si usted instala el
soporte) en el archivo `/etc/snmp/snmpd.conf`.

NOTA: Se incluyen archivos para el agente ZABBIX en el directorio "Goodies".

Si usted desea instalar un "all-in-one", sólo modifique las contraseñas,
direcciones IP y dominios de correo y de *dhcp/dnsmasq* que aparecen en el
archivo de configuración.

Luego de actualizar su archivo de configuración, ejecute en la raíz del
directorio del *script* el comando siguiente:

```
# ./main-installer.sh install
```

El instalador le preguntará si quiere proceder (y/n).

Si ejecuta el instalador con el parámetro adicional *auto*, el mismo seguirá
de manera automática sin preguntar. Ejemplo:

```
# ./main-installer.sh install auto
```

Usted puede guardar todas las salidas del instalador usando la herramienta
`tee`. Ejemplo:

```bash
./main-installer.sh install | tee -a /var/log/my_log_de_install.log
```

Si su nodo de controller va a incluir un servicio de compute (controller +
compute), la siguiente variable del archivo de configuración debe estar en
"no":

```bash
nova_without_compute="no"
```

Si usa ceilometer en el controller, y de la misma manera el controller incluye
el servicio de compute, la siguiente variable debe estar en "no":

```bash
ceilometer_without_compute="no"
```

En cambio, si va a instalar un controlador "puro" (sin servicio de compute)
coloque las variables en "yes":

```bash
nova_without_compute="yes"
ceilometer_without_compute="yes"
```


**Nodos de compute:** Para los nodos de compute, debe dejar en "yes" sólo las
variables de instalación de los módulos de nova y neutron. El resto de los
módulos (glance, cinder, horizon, etc.) deben estar en "no".  Adicionalmente,
las siguiente variables en las secciones de nova y neutron deben estar en
"yes":

```bash
nova_in_compute_node="yes"
neutron_in_compute_node="yes"
```

Y si está usando ceilometer también la siguiente variable debe estar en "yes" para
los nodos de compute:

```bash
ceilometer_in_compute_node="yes"
```

Debe colocar las IP's de los servicios de neutron, keystone, glance y cinder
según la que tiene el controlador (incluyendo las Ip's del backend de Base de
Datos). En cambio, las siguientes variables deben ser colocadas a la IP del
nodo de compute:

```bash
novahost="IP del Controlador"
glancehost="IP del Controlador"
cinderhost="IP del controlador"
neutronhost="IP del controlador"
keystonehost="IP del controlador"
messagebrokerhost="IP del controlador"
dbbackendhost="IP del controlador o del backend de base de datos"
vncserver_controller_address | spiceserver_controller_address = "IP del controlador"
```

Si usa ceilometer, se aplica el mismo caso:

```bash
ceilometerhost="IP del Controlador"
```

Adicionalmente, debe colocar las siguientes variables con la IP del nodo de compute:

```bash
neutron_computehost="IP del Nova Compute Host"
nova_computehost="IP del Nova Compute Host"
```

### Backend de Base de Datos

El instalador tiene la posibilidad de instalar y configurar el backend de base de
datos, y de crear las bases de datos. Esto es completamente controlable por el archivo
de configuración a través de las siguientes variables:

```bash
dbcreate="yes"
dbinstall="yes"
dbpopulate="yes"
```

Con estas tres opciones en "yes", se instalará el software de base de datos,
se configurará y se crearán las bases de datos, todo con la información
contenida en el archivo de configuración.

> **ALERTA**: Si usted elige estas opciones, se debe asegurar que no exista
> previamente software de base de datos instalado o el proceso fallará.

Si usted desea "no instalar el software" pero si tiene acceso administrativo
completo al backend de base de datos, coloque las siguiente combinación:

```bash
dbcreate="yes"
dbinstall="no"
dbpopulate="yes"
```

Con esto, el software de base de datos no será instalado, pero queda de parte
de usted (o su *DBA*) asegurarse que tiene acceso administrativo completo para
crear y modificar bases de datos en el backend seleccionado.

Si no desea ni instalar ni crear bases de datos (asumimos que ya las tiene
previamente creadas) coloque los tres valores en "no":

```bash
dbcreate="no"
dbinstall="no"
dbpopulate="no"

```

### Backend de Mensajería (Message Broker)

Como parte de los componentes a instalar y configurar, este instalador instala
y configura el software para *AMQP* (el *Message Broker*). Esto es un paso
mandatorio para un controlador o un *all-in-one*. Si su o sus servidores ya
tienen un messaje broker instalado, pueden ocurrir conflictos que prevengan el
correcto funcionamiento de la instalación.


### Administrador de Consola (NOVNC/SPICEHTML5)

Mediante una opción configurable en ./configs/main-config.rc (consoleflavor), usted
puede elegir que administrador de consola a usar (NoVNC o SpiceHTML5). Le sugerimos
usar NoVNC que da menos problemas con configuraciones de teclado no us-english y es
mas fácil de reconfigurar para SSL.


### Trove

Este instalador tiene la opción de instalar Trove (ya mas estable a partir de OS-JUNO).
El módulo de instalación de Trove hace la configuración base de Trove pero NO CREA las
imágenes ni reconfigura los datastores para dichas imágenes. Eso le toca a usted como
administrador de la nube de OpenStack (jejeje).


### Scripts de Ayuda

Este instalador colocará en /usr/local/bin un script de ayuda para poder levantar, bajar,
desactivar, activar los servicios de openstack:

```bash
openstack-control.sh OPCIÓN
```

El script utiliza las siguientes opciones:

1. **enable**: activa los servicios para autoarranque en el boot del servidor.
2. **disable**: desactiva los servicios para autoarranque en el boot del servidor.
3. **start**: arranca todos los servicios.
4. **stop**: detiene todos los servicios.
5. **restart**: reinicia todos los servicios.
6. **status**: muestra el estado de todos los servicios.

    > **IMPORTANTE**: El script "openstack-control.sh" tiene la gran ventaja de subir (o
    > bajar) todos los servicios de openstack en el orden correcto. Tanto los
    > paquetes de debian/ubuntu como los de centos colocan el orden no precisamente
    > "óptimo". Recomendación: colocar lo siguiente en el /etc/rc.d/rc.local del
    > servidor para forzar a que los servicios de OpenStack arranquen en el orden
    > correcto:

```bash
/usr/local/bin/openstack-control.sh restart
```

> NOTA: El script detecta que servicios de OpenStack fueron instalados y
> configurados por el instalador para
> iniciar/detener/reiniciar/habilitar/deshabilitar/verificar los servicios
> correctos en el orden correcto.

Adicional a `openstack-control.sh`, el instalador copia a `/usr/local/bin` el
script `openstack-log-cleaner.sh`.  Este script tiene como función limpiar
todos los logs de todos los componentes de *OpenStack* instalados por esta
herramienta de instalación.

El script es llamado durante la fase final de instalación para limpiar los
logs antes de dejar el servidor instalado, pero puede ser utilizado también
para limpiar los logs en caso de ser necesario.

NOTA IMPORTANTE: Recomendamos usar el script openstack-control.sh para inicializar
todos sus servicios de openstack !. Coloque todos los servicios en "disable" con
"openstack-control.sh disable" y llame al script con la opción "start" desde
el /etc/rc.local del sistema operativo !.

### ARRANQUE CONTROLADO DE MAQUINAS VIRTUALES

Script "openstack-vm-boot-start.sh": Este script sirve para levantar las VMs
de manera controlada y con tiempos de espera entra cada inicio de VM con el fin
de evitar "tormentas" de I/O. El script utiliza el siguiente archivo de
configuración:

```bash
/etc/openstack-control-script-config/nova-start-vms.conf
```

Coloque en dicho archivo los nombres de las VMs que quiere arrancar de manera
ordenada y secuencial para evitar tormentas de I/O. El script puede ser llamado
desde el "/etc/rc.local" del sistema operativo.

NOTA: Los nombres de las VMs se deben obtener del comando "nova list".


### DNSMASQ

El instalador crea una configuración personalizada del componente *dnsmasq*
usado por el agente *DHCP* de *Neutron* (`neutron-dhcp-agent`). Dicha configuración
incluye un archivo donde usted puede colocar opciones especiales:

```
/etc/dnsmasq-neutron.d/neutron-dnsmasq-extra.conf
```

Hay ejemplos comentados en el archivo. Use esos ejemplos para pasar opciones a
las distintas instancias de dnsmasq creadas para cada subred donde usted
active la opción de usar *dhcp*.

> **Recomendación**: Trate de tener una buena estructura de "DNS" para sus máquinas
> virtuales de manera que las pueda identificar de manera apropiada y utilice
> las opciones de dnsmasq para agregar o separar subdominios para cada rango de
> direcciones IP.


### Modularización del Instalador

Si bien el proceso de instalación principal "*main-installer*" se encarga de
llamar a cada módulo de cada componente del instalador, dichos módulos son
realmente independientes entre si, al punto de que pueden ser llamados de
manera secuencial. No es el caso común, pero puede hacerse. El orden normal de
ejecución de cada módulo es el siguiente (asumiendo que todos los componentes
serán instalados):

* requeriments.sh
* messagebrokerinstall.sh
* databaseinstall.sh
* requeriments-extras.sh (sólo presente para Debian 7 y Ubuntu Server 14.04 LTS)
* keystoneinstall.sh
* swiftinstall.sh
* glanceinstall.sh
* cinderinstall.sh
* neutroninstall.sh
* novainstall.sh
* ceilometerinstall.sh
* heatinstall.sh
* troveinstall.sh
* saharainstall.sh
* snmpinstall.sh
* horizoninstall.sh
* postinstall.sh

Si desea ejecutar los módulos en orden sin usar el instalador principal, debe
ejecutarlos desde el directorio donde se encuentra el instalador, de la siguiente
manera:

```
# ./modules/Modulo-a-ejecutar.sh
```

Todos los módulos leen el archivo de configuración
(`./configs/main-config.rc`) y tomarán las opciones de configuración desde
dicho archivo.

Cada módulo que se ejecuta de manera exitosa dejará una serie de archivos de
control en el directorio siguiente:

```
/etc/openstack-control-script-config
```

Dichos archivos de control son utilizados por los módulos para evitar una
re-ejecución de los mismos que pueda causar problemas en la instalación de
OpenStack, y también son utilizados por el script "openstack-control.sh" para
saber que componentes de OpenStack fueron instalados de manera exitosa y que
servicios están instalados para iniciar/detener/reiniciar/etc.


### RECOMENDACIONES DE INSTALACIÓN PARA CENTOS Y DEBIAN.

#### Centos 6:

Lamentablemente, dado que RDO no ha publicado (aún) paquetes de OpenStack JUNO para
Centos 6, no tenemos como soportar esta versión del Sistema Operativo.


#### Centos 7:

1. Instale centos con la selección de paquetes para "Infraestructure Server" (ser-
   vidor de infraestructura). Asegúrese de tener correctamente instalado, configu-
   rado y operativo el servicio ntpd. Ser recomienda también usar ntpdate.

2. Agregue los repositorios EPEL y RDO (ver "NOTAS.txt").

3. Instale y configure OpenVSWitch (de nuevo, ver "NOTAS.txt").

ALERTA: Esta versión de OpenStack no soporta MySQL menor a 5.5. Vea las notas
y tome sus precauciones !.

Si usted va a usar un manejador de base de datos externo basado en MySQL/MariaDB,
ASEGURESE que sea la versión correcta (5.5) para no terminar con una instalación
de OpenStack inservible !.

NOTA IMPORTANTE: El instalador de Centos 7 desactiva SELINUX. Esto se requiere para
evitar problemas encontrados especialmente cuando se utiliza PostgreSQL como backend
de base de datos y con NOVA-API. Cuando estos bugs sean corregidos en los paquetes de
RDO, se volverá a reactivar SELINUX. Por lo pronto, lo desactivamos desde el módulo 
de requerimientos.


#### Debian 7:

1. Instale debian con la selección de paquetes "Standard System Utilities"
(utilitarios de sistema estandard) y con SSH Server (servidor ssh). Asegúrese
de tener correctamente instalado, configurado y operativo el servicio ntpd. Se
recomienda también usar ntpdate.

2. Agregue el repositorio de OpenStack para Debian y asegúrese de tener las ramas completas
para sus repos de debian (ver "NOTAS.txt").

3. Instale y configure OpenVSWitch (de nuevo, ver "NOTAS.txt").


#### Ubuntu 14.0.4 LTS:

1. Instale Ubuntu Server 14.04 LTS de manera estandar y seleccione como paquete adicional
"OpenSSH Server". Instale y configure el servicio ntpd. Se recomienda también usar ntpdate.

2. Instale y configure OpenVSWitch (ver "NOTAS.txt").


### Cinder:

Si va a usar CINDER con lvm-iscsi, asegúrese de tener una partición o disco libre para crear
un LVM llamado "cinder-volumes". Ejemplo (disco libre /dev/sdc):

```bash
pvcreate /dev/sdc
vgcreate cinder-volumes /dev/sdc
```

Otro ejemplo con una partición libre /dev/sda3:

```bash
pvcreate /dev/sda3
vgcreate cinder-volumes /dev/sda3
```

### Swift:

Si va a usar swift, recuerde que debe tener el disco/partición de swift montado sobre un
directorio específico y este debe ser indicado en la configuración del instalador
(main-config.rc).

Ejemplo:

Variable `swiftdevice="d1"`

En el fstab "d1" debe estar montado así:

```
/dev/sdc1 /srv/node/d1 ext4 acl,user_xattr 0 0
```

En este ejemplo, se asume que existe ya una partición "/dev/sdc1" previamente formateada
en ext4 o cualquier otro sistema de archivos soportado por Linux.


### Arquitectura:

Ya sea que use Centos, Debian o Ubuntu, debe elegir utilizar 64 bits
(amd64/x86_64). No trate de instalar OpenStack en 32 bits.


### Servicio NTP:

Es VITAL que sus servidores de OpenStack tengan una correcta sincronización de
tiempo o habrá serios problemas entre el controller y los nodos de
compute. Lea la documentación de OpenStack para saber mas al respecto.


### Recomendaciones para Virtualbox.

Usted puede usar este instalador en una VM de VirtualBox si no desea usar un
servidor "real" para practicar y aprender OpenStack. Debería tener un "mínimo
absoluto" de 2GB's de RAM en su equipo "real" y asignar al menos 900 Mb's de
RAM a la VM de VirtualBox, pero si quiere hacer una prueba mas extensa, trate
de tener una VM con al menos 4 GB's.


### Recomendaciones de hardware para una VM de VirtualBox:

Discos Duros: Uno para el sistema operativo (16 Gb's mínimo), uno para
Cinder-Volumes y otro para swift - espacio variable... mínimo 8GB's para cada
disco (switf y cinder-volumes).  Red: tres interfaces:
 * Interfaz 1 en modo NAT para salida a Internet.
 * Interfaz 2 en modo "host only adapter, promisc: todos", para poder
   administrar el Servidor OpenStack - sugerencia: Usar vboxnet0 con la red
   192.168.56.0/24 (desactivar el dhcp de virtualbox) y asignarle la IP
   192.168.56.2 a la interfaz (la .1 estará en la máquina real).
 * Interfaz 3 en modo "host only adapter, promiscq:q: todos", para poder
   asignar a las VM's de OpenStack la red en la interfaz eth2 y el rango IP
   192.168.57.0/24 (la IP 192.168.57.1 estará en la máquina real).

Hacer la instalación del S/O de 64 bits de su preferencia. Agregar los
repositorios y soporte ntp según las recomendaciones en este documento, crear
el switch de OpenVSWITCH br-int, crear el switch de OpenVSWITCH br-eth2 y
agregarle el puerto eth2 (la interfaz 3 en la VM de VirtualBox).

Crear el volumen de cinder contra el segundo disco duro de la VM de
virtualbox:

```bash
pvcreate /dev/sdb
vgcreate cinder-volumes /dev/sdb
```

Si va a usar swift, crear la partición en el tercer disco (/dev/sdc1) y
montarla según las notas en este documento.

Hacer la instalación indicando que el Mapping de bridge (dentro de
main-config.rc) es:

```bash
bridge_mappings="publica:br-eth2"
```

Cambiar la IP en el `main-config.rc` a la IP asignada a la VM en la red
192.168.57.0/24.

Ejecutar el instalador.

Disfrutar de OpenStack :-)

Usted podrá entrar al servidor vía web por la interfaz 192.168.56.x para
ejecutar las tareas de administración de OpenStack. Creé su subred en el rango
de eth2 (192.168.57.0/24) y podrá entrar a las VM's de OpenStack desde su
máquina real que tendrá la interfaz 192.168.57.1.


### Desinstalación

El script principal tiene también un parámetro que llama al módulo de desinstalación:

```
# ./main-installer.sh uninstall
```
o

```
# ./main-installer.sh uninstall auto
```

La primera forma de llama al proceso de desinstalación, preguntará "y/n" para
proseguir o abortar, pero al ser llamado con el parámetro extra "auto", no
habrá preguntas y todo lo que el instalador instaló será eliminado del
servidor.

Es importante tener en cuenta que si se utilizó la opción dbinstall="yes", el
desinstalador eliminará no solamente el manejador de base de datos sino
también las bases de datos creadas.

Si usted desea NO ELIMINAR las bases de datos creadas, modifique el
"main-config.rc" y coloque la opción dbinstall="no". Esto hará que el
desinstalador no elimine ni el manejador de base de datos ni las bases de
datos creadas.

ALERTA: Si usted no tiene cuidado, podría terminar eliminando bases de datos
de otras aplicaciones !. Queda advertido !.

Esto es muy conveniente para una reinstalación. Si por alguna razón su
instalación de OpenStack requiere ser reconstruida sin tocar las bases de
datos o el manejador, desinstale usando dbinstall="no", y cuando vaya a
reinstalar, coloque todas las opciones de base de datos en "no" para conservar
tanto el manejador como las bases de datos y data creada:

```
dbcreate="no"
dbinstall="no"
dbpopulate="no"
```

Si su instalación tiene múltiples nodos (controller / compute) use los
archivos `main-config.rc` con los que instaló cada nodo para la desinstalación
del nodo correspondiente.


### Goodies

En el directorio *Goodies* usted podrá encontrar algunos scripts (cada uno con
su respectivo readme) que puede utilizar con su instalación de OpenStack. Vea
los scripts y sus respectivos "readmes" para entender mejor como usarlos !.


### Notas Finales

Este instalador fue orientado inicialmente al modelo de red flat/vlan's con
router externos donde el módulo de red (Neutron) no canalizará tráfico (sólo
manejará los recursos de puertos de ovs, lbaas, fwaas, vpnaas y levantará las
configuraciones necesarias). En este modelo, neutron "no se convierte" en un
posible cuello de botella para el tráfico de red. Sin embargo, usted "si tiene
los conocimientos de configuración de openstack" puede adaptar la configuración 
y/o los módulos a sus necesidades en caso de querer utilizar el modelo de
tunneling o cualquier otra configuración de Neutron que requiera.

### FIN.-
