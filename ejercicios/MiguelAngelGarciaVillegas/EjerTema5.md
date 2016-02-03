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

Voy a realizar también la instalación de un lubuntu, desde Qemu.

añadimos disco virtual: ***qemu-img create -f qcow2 lubuntu.qcow2 4G***

Ejecutamos ***qemu-system-x86_64 -hda lubuntu.qcow2 -cdrom ~/Escritorio/Curso15-16/IV/EjerTema5/ejer4/lubuntu-12.04-desktop-i386.iso -m 512M*** para llevar a cabo la instalación.

![Lubuntu ](https://www.dropbox.com/s/zanjre1p4mla3da/04.1.png?dl=1)

![Instalación Lubuntu ](https://www.dropbox.com/s/z5muccqzxfqxrku/04.3.png?dl=1)

![Instalación Lubuntu ](https://www.dropbox.com/s/68nygdpivu19xmy/04.4.png?dl=1).

## Ejercicio 2.2
### Hacer un ejercicio equivalente usando otro hipervisor como Xen, VirtualBox o Parallels.

Vamos a utiliza VirtualBox y vamos a volver a instalar Slitaz.

Abrimos VirtualBox y le damos a Nueva, ponemos el nombre, la configuración, tamaño en la memoria, disco duro, tipo de archivo de disco duro, almacenamiento, ubicación de archivo y tamaño.

![VirtualBox Nueva](https://www.dropbox.com/s/szs3fexm0uqpkqy/3.1.png?dl=1)


![VirtualBox Disco Duro y tipo archivo](https://www.dropbox.com/s/g0522c6j3gzpyeq/3.02.png?dl=1)

Ahora iniciamos

![Corriendo](https://www.dropbox.com/s/nnaujdmwcmjchax/3.3.png?dl=1)

![Corriendo](https://www.dropbox.com/s/mvbwkhsvx3vcqds/3.4.png?dl=1)

## Ejercicio 3.
### Crear un benchmark de velocidad de entrada salida y comprobar la diferencia entre usar paravirtualización y arrancar la máquina virtual simplemente con qemu-system-x86_64 -hda /media/Backup/Isos/discovirtual.img

Para realizar éste ejercicio vamos a hacer uso de ***sysbench*** que permite evaluar la potencia de I/O de los discos

Para ello vamos a instalarlo.

![instalación](https://www.dropbox.com/s/sbee7z2skl0c1j3/03.1.png?dl=1)

Una vez instalado, en nuestro caso vamos a crear los ficheros para el test de 8GB (mayor que la RAM), ejecutando en la terminal el siguiente comando ***sysbench --test=fileio --file-total-size=8G prepare***

![Creando ficheros de test ](https://www.dropbox.com/s/o2yj6pskd8uls2g/03.2.png?dl=1)
Una vez creados, ya sólo nos queda ejecutar el test y esperar por lo resultados.

## Ejercicio 4.
### Crear una máquina virtual Linux con 512 megas de RAM y entorno gráfico LXDE a la que se pueda acceder mediante VNC y ssh.

Arrancamos ahora mediante servidor VNC ejecutando en el terminal: ```qemu-system-i386 -hda lubuntu.img vnc :1```

Y con la versión de Lubuntu descargada, vamos a iniciar el SO con Qemu: ```qemu-system-x86_64 -hda lubuntu.img -cdrom lubuntu-15.10-desktop-amd64.iso -m 512M``` e instalamos.

![Instalación Lubuntu Ejer4](https://www.dropbox.com/s/nub41un21r0iio0/ejer%204.5.png?dl=1)

![Instalación Lubuntu Ejer4](https://www.dropbox.com/s/pv8bqv0869wic9o/Ejer4.6.png?dl=1)


Para acceso VNC:

Configurando según la orden, ejecutamos: ***qemu-system-i386 -hda lubuntu.img vnc :1***

Ahora vamos a conectar a la máquina virtual usando algún cliente de VNC tal como vinagre, para ello ejecutamos en el terminal, ***sudo apt-get install vinagre***

Nnos podemos conectar a la máquina con vinagre: ***vinagre localhost:5901***



Para conectar por SSH:

Primero redireccionamos el puerto: ***qemu-system-x86_64 -boot order=c -drive file=lubuntu.img,if=virtio -m 512M -name magv -redir tcp:2222::22.***

Y conectamos: ***ssh -p 2222 magv@localhost***.

## Ejercicio 5.
### Crear una máquina virtual ubuntu e instalar en ella un servidor nginx para poder acceder mediante web.


Error al instalar nodejs-legacy
https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial/

## Ejercicio 6.
### Usar juju para hacer el ejercicio anterior.

## Ejercicio 7.
### Instalar una máquina virtual con Linux Mint para el hipervisor que tengas instalado.

Vamos a utiliza VirtualBox y vamos a volver a instalar Linux Mint.

Abrimos VirtualBox y le damos a Nueva, ponemos el nombre, la configuración, tamaño en la memoria, disco duro, tipo de archivo de disco duro, almacenamiento, ubicación de archivo y tamaño.

![VirtualBox Nueva](https://www.dropbox.com/s/f9a74wjonrsep9i/7.0.png?dl=1)

Ahora iniciamos

![Corriendo](https://www.dropbox.com/s/rtkapkwur0ei0z5/7.1.png?dl=1)


Ahora vamos a realizar con Qemu.

Añadimos disco virtual: ***qemu-img create -f qcow2 linuxmint.qcow2 6G***

Ejecutamos ***qemu-system-x86_64 -hda linuxmint.qcow2 -cdrom ~/Escritorio/Curso15-16/IV/EjerTema5/ejer7/linuxmint-17.1-cinnamon-32bit.iso*** para llevar a cabo la instalación.

![comandos](https://www.dropbox.com/s/vw413w4t8w1qdhb/7.png?dl=1)
