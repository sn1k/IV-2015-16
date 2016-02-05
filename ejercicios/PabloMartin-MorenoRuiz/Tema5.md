# Uso de sistemas de virtualización

Estas prácticas las he desarrollado en el ordenador de un compañero de 64 bits dónde creamos otra cuenta

## Ejercicio 1. Instalar los paquetes necesarios para usar KVM. Se pueden seguir estas instrucciones. Ya lo hicimos en el primer tema, pero volver a comprobar si nuestro sistema está preparado para ejecutarlo o hay que conformarse con la paravirtualización.

Primero tenemos que instalar el siguiente paquete: sudo apt-get install cpu-checker

Ejecutamos el siguiente comando para comprobar comprobar que tenemos paravirtualización:

![comprobacionkvm](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/Seleccioacuten_001_zpsfstijrg7.png)

Instalamos los siguientes paquetes para tener KVM:
```
sudo apt-get install qemu-kvm libvirt-bin ubuntu-vm-builder bridge-utils
```

Para crear máquinas virtuales instalamos el siguiente paquete:
```
sudo apt-get install virtinst
```

Ahora añado mi usuario a los siguientes grupos:

![grupos](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/Seleccioacuten_002_zpshlro1hrw.png) 

Reinicio

Y ahora compruebo que esta bien instalado:

![funciona](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/Seleccioacuten_003_zpsmhcjt3x4.png)

Podemos instalar una interfaz gráfica con el siguiente comando:
```
sudo apt-get install virt-manager
```
Y aquí la tenemos:
![InterfazGraficaQemu](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/Seleccioacuten_004_zpsu9d4rfqe.png)

## Ejercicio 2.

### 1. Crear varias máquinas virtuales con algún sistema operativo libre tal como Linux o BSD. Si se quieren distribuciones que ocupen poco espacio con el objetivo principalmente de hacer pruebas se puede usar CoreOS (que sirve como soporte para Docker) GALPon Minino, hecha en Galicia para el mundo, Damn Small Linux, SliTaz (que cabe en 35 megas) y ttylinux (basado en línea de órdenes solo).

### 2. Hacer un ejercicio equivalente usando otro hipervisor como Xen, VirtualBox o Parallels. 

## Ejercicio 3. Crear un benchmark de velocidad de entrada salida y comprobar la diferencia entre usar paravirtualización y arrancar la máquina virtual simplemente con qemu-system-x86_64 -hda /media/Backup/Isos/discovirtual.img

## Ejercicio 4. Crear una máquina virtual Linux con 512 megas de RAM y entorno gráfico LXDE a la que se pueda acceder mediante VNC y ssh.

## Ejercicio 5. Crear una máquina virtual ubuntu e instalar en ella un servidor nginx para poder acceder mediante web.


## Ejercicio 7. Instalar una máquina virtual con Linux Mint para el hipervisor que tengas instalado.