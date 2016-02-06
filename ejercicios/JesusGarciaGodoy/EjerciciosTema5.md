# Ejercicios Tema 5

## Ejercicio 1

**Instalar los paquetes necesarios para usar KVM. Se pueden seguir estas instrucciones. Ya lo hicimos en el primer tema, pero volver a comprobar si nuestro sistema está preparado para ejecutarlo o hay que conformarse con la paravirtualización.**

Para comprobar si los paquetes están instalados ejecutamos:

```
	egrep '(vmx|svm)' --color=always /proc/cpuinfo
```

También se puede hacer con el siguiente comando, en donde si el valor mostrado es mayor que 0 indica que, efectivamente, la virtualización está soportada.

```
	egrep -c '(vmx|svm)' /proc/cpuinfo
```


![comprobarvmx](http://i.imgur.com/JEuYqYT.png)

A continuación instalamos los paquetes necesarios con:

```
	sudo apt-get install kvm qemu-kvm libvirt-bin virtinst
```


Seguidamente, añadimos nuestro usuario a los grupos `libvirtd` y `kvm`:

```
	sudo adduser `id -un` libvirtd
	sudo adduser `id -un` kvm
```

Pasamos a reiniciar los módulos de KVM:

```
	rmmod kvm
	modprobe -a kvm
```

Finalmente comprobamos que el resultado del siguiente comando no nos da error:

```
	sudo virsh -c qemu:///system list
```


## Ejercicio 2.1

**Crear varias máquinas virtuales con algún sistema operativo libre tal como Linux o BSD. Si se quieren distribuciones que ocupen poco espacio con el objetivo principalmente de hacer pruebas se puede usar CoreOS (que sirve como soporte para Docker) GALPon Minino, hecha en Galicia para el mundo, Damn Small Linux, SliTaz (que cabe en 35 megas) y ttylinux (basado en línea de órdenes solo).**


**Debian**

Creamos una imagen de disco virtual con: 

```
qemu-img create -f qcow2 ~/maquinas/debian.qcow 2G
```

Descargamos la [ISO](https://www.debian.org/index.es.html) Debian y ejecutamos:

```
 qemu-system-x86_64 -machine accel=kvm -hda debian.qcow2 -cdrom debian-8.3.0-amd64-CD-1.iso -m 1G -boot d
```

![maquinaDebian](http://i.imgur.com/sanlQ5C.png)


**SLiTaz**

Creamos una imagen de disco virtual:
```
jesmorc@jesmorc-PClaptop ~ $ qemu-img create -f qcow2 slitaz.qcow2 2G
Formatting 'slitaz.qcow2', fmt=qcow2 size=2147483648 encryption=off cluster_size=65536 lazy_refcounts=off 

```

Descargamos la [ISO](http://www.slitaz.org/en/) y ejecutamos la siguiente línea para la instalación:

```
jesmorc@jesmorc-PClaptop ~ $ qemu-system-x86_64 -machine accel=kvm -hda slitaz.qcow2 -cdrom slitaz-5.0-rc3.iso -m 1G -boot dd

```

![maquinaSLiTaz](http://i.imgur.com/wRT62bk.png)




## Ejercicio 2.2

**Hacer un ejercicio equivalente usando otro hipervisor como Xen, VirtualBox o Parallels.**

Instalaré **SLliTaz** dada su ligereza, usando **VirtualBox**.

Tal y como vemos a lo largo de las siguienets imágenes, creamos una nueva máquina, asignando la RAM que vaya a usar.
Después creamos un disco duro virtual VDI con el tamaño que queramos.
Finalmente le montamos la ISO en la cargadora de CD virtual y la arrancamos.
![vbox_slitaz](http://i.imgur.com/CkdfuSE.png)
![vbox_slitazhdd](http://i.imgur.com/1GDPOah.png)
![vbox_slitazisomount](http://i.imgur.com/oleVRCF.png)
![vbox_slitazrunning](http://i.imgur.com/3h0jJZt.png)


## Ejercicio 3

**Crear un benchmark de velocidad de entrada salida y comprobar la diferencia entre usar paravirtualización y arrancar la máquina virtual **

El benchmark simplemente ejecutará funciones matemáticas que requieren uso computacional moderado.

**benchmark.py**:
```
import math
d = {}
for i in range(1, 9999999):
        d[i] = math.log(i)
```


Para ejecutar el algoritmo en la máquina virtual slitaz en modo normal hacemos:

```
qemu-system-x86_64 -hda slitaz.qcow
```

Con la opción "virtio" indicamos que se use la paravirtualización.

```
 emu-system-x86_64 -boot order=c -drive file=slitaz.qcow,if=virtio
```

En cada uno he realizado lo siguiente, utilizando la librería *time* de python:
```
import time
start_time = time.time()
python benchmark.py
print("--- %s seconds ---" % (time.time() - start_time))
```
La conclusión es que los tiempos no difieren mucho, pero van algo más rápido en el modo normal.


## Ejercicio 4

**Crear una máquina virtual Linux con 512 megas de RAM y entorno gráfico LXDE a la que se pueda acceder mediante VNC y ssh.**

Para que unix tenga entorno gráfico LXDE, vamos a instalar la distrubución Lubuntu. [ISO](http://cdimage.ubuntu.com/lubuntu/releases/14.04/release/).

Igual que anteriormente, primero se crea el disco virtual: 
```
qemu-img create -f qcow2 lubuntu.qcow2 5G
```

Seguido de :

```
qemu-system-x86_64 -hda lubuntu.qcow2 -cdrom ./lubuntu-14.04.3-desktop-i386.iso -m 512M
```

Para configurar el acceso VNC, procedemos a instalar "vinagre":

```
sudo apt-get install vinagre
```

Para acceder:

```
vinagre localhost:1
```

Ahora instalamos y configuramos SSH:

```
sudo apt-get install ssh
```

Arrancamos la máquina lubuntu con puerto 2150:

```
qemu-system-x86_64 -hda lubuntu.qcow2 -m 512M -redir tcp:2150::22
```
*(22 del final es el puerto por defecto de SSH)*

Ahora podremos acceder por ssh a la máquina con:
```
ssh jesmorc@localhost -p 2121
```

![ejtema5_ej4](http://i.imgur.com/2Uco5RH.png)





