# Asignatura: IV Grupo de Practicas Miercoles 8:30h a 10:30h
## Miguel Ángel García Villegas

# Ejercicios Tema 5

## Ejercicio 1.
### Instalar los paquetes necesarios para usar KVM. Se pueden seguir estas instrucciones. Ya lo hicimos en el primer tema, pero volver a comprobar si nuestro sistema está preparado para ejecutarlo o hay que conformarse con la paravirtualización.

Para instalarlo hay que ejecutar en el terminal la instrucción, ***sudo apt-get install cpu-checker***
![sudo apt-get install cpu-checker](https://www.dropbox.com/s/j3vplffz19hl3iv/01.1.png?dl=1)

Podemos comprobar que nuestro sistema esta preparado para ejecutarlo mediante la orden ***kvm-ok*** o la orden ***egrep -c '(vmx|svm)' /proc/cpuinfo*** si sale un número diferente a 0, indica que la virtualización está soportada.

![kvm-ok](https://www.dropbox.com/s/dg3jvt3yzftdjow/01.2.png?dl=1)

Para instalar los paquetes necesarios, podemos hacerlo mediante la orden ***sudo apt-get install qemu-kvm libvirt-bin virtinst kvm virt-viewer***
![sudo apt-get install qemu-kvm libvirt-bin virtinst kvm virt-viewer](https://www.dropbox.com/s/7tx0a1hh566szrq/01.3.png?dl=1)

Una vez instalados, es necesario indicar el usuario que queremos que utilice la virtualización ***sudo adduser `id -un` libvirtd***

A continuación se tiene que añadir el usuario a los grupos libvirtd y kvm con los siguientes comandos, ***sudo adduser `id -un` libvirtd*** y  ***sudo adduser `id -un` kvm***

![comandos](https://www.dropbox.com/s/coo1a4szqxl3i2i/01.4.png?dl=1)


## Ejercicio 2.1
### Crear varias máquinas virtuales con algún sistema operativo libre tal como Linux o BSD. Si se quieren distribuciones que ocupen poco espacio con el objetivo principalmente de hacer pruebas se puede usar CoreOS (que sirve como soporte para Docker) GALPon Minino, hecha en Galicia para el mundo, Damn Small Linux, SliTaz (que cabe en 35 megas) y ttylinux (basado en línea de órdenes solo).

Comenzamos activando KVM con: ***sudo modprobe kvm-intel***

Primero vamos a crear una máquina virtual con SliTaz: Necesitamos una imagen Iso.

Creamos un disco duro virtual en formato QCOW2:
***qemu-img create -f qcow2 fichero-cow.qcow2 200M***

![qemu-img create -f qcow2 fichero-cow.qcow2 200M](https://www.dropbox.com/s/9yoeeropfngufw2/2.01.png?dl=1)

Instalamos el sistema con el fichero de almacenamiento virtual creado y la ISO descargada, usando KVM mediante: ***qemu-system-x86_64 -hda fichero-cow.qcow2 -cdrom slitaz-4.0.iso***

![qemu-system-x86_64 -hda fichero-cow.qcow2 -cdrom slitaz-4.0.iso](https://www.dropbox.com/s/nglrj2pqfzj7yai/2.02.png?dl=1)

![Qemu](https://www.dropbox.com/s/gu77jgm66ibccrn/02.3.png?dl=1)

Ahora vamos a crear uno en Ubuntu

Creamos un disco duro virtual en formato QCOW2:

***qemu-img create -f qcow2 ubuntu.qcow2 8G***

Instalamos el sistema con el fichero de almacenamiento virtual creado y la ISO descargada, usando KVM mediante:
***qemu-system-x86_64 -machine accel=kvm -hda ubuntu.qcow2 -cdrom ubuntu-14.04.1-desktop-amd64.iso -m 1G -boot d***

![Qemu Ubuntu](https://www.dropbox.com/s/y7mz9mbmptt9b9v/2.4.png?dl=1)


## Ejercicio 2.2
### Hacer un ejercicio equivalente usando otro hipervisor como Xen, VirtualBox o Parallels.

## Ejercicio 3.
### Crear un benchmark de velocidad de entrada salida y comprobar la diferencia entre usar paravirtualización y arrancar la máquina virtual simplemente con qemu-system-x86_64 -hda /media/Backup/Isos/discovirtual.img

## Ejercicio 4.
### Crear una máquina virtual Linux con 512 megas de RAM y entorno gráfico LXDE a la que se pueda acceder mediante VNC y ssh.

## Ejercicio 5.
### Crear una máquina virtual ubuntu e instalar en ella un servidor nginx para poder acceder mediante web.

## Ejercicio 6.
### Usar juju para hacer el ejercicio anterior.

## Ejercicio 7.
### Instalar una máquina virtual con Linux Mint para el hipervisor que tengas instalado.
