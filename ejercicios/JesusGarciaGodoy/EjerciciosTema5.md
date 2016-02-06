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






