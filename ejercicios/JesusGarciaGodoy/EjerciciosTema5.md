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






