#Ejercicios - Jesús Prieto López
##TEMA 4

###Ejercicio 1: Instalar los paquetes necesarios para usar KVM. Se pueden seguir [estas instrucciones](https://wiki.debian.org/KVM#Installation). Ya lo hicimos en el primer tema, pero volver a comprobar si nuestro sistema está preparado para ejecutarlo o hay que conformarse con la paravirtualización.

Para comprobar si nuestro sistema está preparado o no ejecutamos el comando:

`$ kvm-ok`

![Comprobación del uso de kvm](cap1)

Instalamos todos los paquetes necesarios para hacer uso de KVM.

`$ apt-get install qemu-kvm libvirt-bin`


###Ejercicio 2: 
#### Ejercicio 2.1: Crear varias máquinas virtuales con algún sistema operativo libre tal como Linux o BSD. Si se quieren distribuciones que ocupen poco espacio con el objetivo principalmente de hacer pruebas se puede usar CoreOS (que sirve como soporte para Docker) GALPon Minino, hecha en Galicia para el mundo, Damn Small Linux, SliTaz (que cabe en 35 megas) y ttylinux (basado en línea de órdenes solo)

Para este ejercicio he utilizado las distribuciones [Damn Small Linux](http://www.damnsmalllinux.org/download.html) y [Slitaz](http://www.slitaz.org/es/).

Activamos, por si no lo teníamos ya, KVM con el siguiente comando:

`$ modprobe kvm-intel`

Para las máquinas virtuales necesitamos, por ejemplo, discos duros virtuales. En este caso voy a usar discos duros en formato QCOW2 de tamaño de 1 GB.

Vamos a crear la máquina virtual con la distribución *Slitaz*, podemos bajarnos una versión desde la página oficial. Creamos un disco duro para la primera máquina virtual.

`$ qemu-img create -f qcow2 disco1.qcow2 1G`

![Creación de disco virtual qcow2](cap2)

Una vez creado, con la herramienta KVM creamos la máquina virtual con el SO deseado (indicando donde está la ISO guardada) y el fichero del disco duro virtual. En este caso la indico la imagen que me he descargado de la distribución *Slitaz*, concretamente la 4.0.

`$ qemu-system-x86_64 -hda disco1.qcow2 -cdrom slitaz-4.0.iso`

![Arranque de máquina virtual con KVM](cap3)

Ahora vamos a crear otra máquina virtual, con otro SO diferente, *Damn Small Linux*. Repetimos los pasos. 

Creamos el disco virtual para almacenar el sistema.

`$ qemu-img create -f qcow2 disco2.qcow2 1G`

Ahora con la herramienta KVM creamos la máquina virtual indicando  el disco nuevo creado y la distrubición, que es la versión 4.11.rc2. 

`$ qemu-system-x86_64 -hda disc2.qcow2 -cdrom dsl-4.11.rc2.iso`

![Creación de la segunda máquina virtual con KVM](cap4)

#### Ejercicio 2.2: Hacer un ejercicio equivalente usando otro hipervisor como Xen, VirtualBox o Parallels.

He utilizado el hipervisor VMware Player que puedes encontrar en la web de [VMware](http://www.vmware.com/es).

Cuando iniciamos VMware Player aparece una ventana como la siguiente.

![Ventana principal de VMware Player](cap5)

En esta ventana podemos darle a la opción de **Create a New Virtual Machine** para proceder a crear la máquina virtual. Después nos mostrará una serie de pasos para la configuración de la misma.

El paso siguiente será indicar la imagen del sistema a instalar y desde donde cargarlo. En este caso voy a utilizar un ubuntu server que tenía previamente.

![Paso para seleccionar la imagen de la máquina virtual](cap6)

Ahora el paso es para indicarle el tipo de SO que es. Normalmente lo reconoce solo.

![Paso para indicar el tipo de sistema de la máquina virtual](cap7)

En el siguiente paso indicamos cómo llamar a la máquina virtual y donde guardarla en nuestro sistema anfitrión.

![Paso para indicar el nombre y el directorio de la máquina virtual](cap8)

Indicamos en el próximo paso cuanto tamaño tendrá el disco duro virtual para almacenar el sistema.

![Paso para indicar el tamaño de disco de la máquina virtual](cap9)

Por último nos muestra un resumen de las opciones fijadas durante los pasos anteriores, y la posibilidad de moficarlos. Por defecto nos pone una cantidad de RAM de 1GB. Pulsamos el botón **Finish** para finalizar y poder ejecutar la máquina virtual.

![Resumen de configuración de la máquina virtual](cap10)

Y ya podremos iniciar la máquina virtual con normalidad. 

![Máquina virtual arrancada con la distribución de linux server](cap11)


###Ejercicio 4: Crear una máquina virtual Linux con 512 megas de RAM y entorno gráfico LXDE a la que se pueda acceder mediante VNC y ssh.

He utilizado una versión de *Debian* que tiene el entorno gráfico LXDE. La imagen me la he bajado del [siguiente enlace](http://cdimage.debian.org/debian-cd/current-live/i386/iso-hybrid/debian-live-8.2.0-i386-lxde-desktop.iso).

Creamos el disco duro virtual para poder crear la máquina virtual como hemos hecho en ejercicios anteriores.

`$ qemu-img create -f qcow2 disco-debian.qcow2 4G`

Ahora creamos la máquina virtual con la imagen descargada y sobre el disco que hemos creado. Vamos a crearla con 512 megas de RAM, tenemos que indicarlo con la opción **-m**.

`$ qemu-system-x86_64 -hda disco-debian.qcow2 -cdrom debian-live-8.2.0-i386-lxde-desktop.iso -m 512M`

Como queremos acceder mediante VNC, necesitamos descargar un cliente (de ssh ya viene por defecto en la distribuciones de linux, o es lo normal). Podemos instalar y usar el cliente **vinagre**.

`$ apt-get install vinagre`

Ahora hay que iniciar la máquina virtual dentro de un servidor VNC. La siguiente orden indica como hacerlo.

`$ qemu-system-x86_64 -hda disco-debian.qcow2 -vnc :1`

Como hemos indicado un 1 en el comando para arrancar la máquina virtual en servidor VNC tenemos que conectarnos con el puerto 5901.

`$ vinagre localhost:5901`

Y nos aparece una ventana donde podemos acceder a nuestra máquina virtual.

![Máquina virtual a través del cliente de VNC vinagre](cap13)



