### Ejercicio 1
Lo primero que vamos a hacer es instalar los programas necesarios, ya que Ubuntu no trae por defecto el comando kvm-ok, de modo que ejecutamos lo siguiente:


![10](https://www.dropbox.com/s/7usgjg1pqbnkwir/5-1-001.png?dl=1)
![11](https://www.dropbox.com/s/sshdzrgais8otmd/5-1-002.png?dl=1)

Ahora podemos ver como nuestro pc admite kvm-ok

![12](https://www.dropbox.com/s/hdimweoeuhxsuky/5-1-000.png?dl=1)

Vamos a proceder pues a terminar la instalación, para ello ejecutamos lo siguiente:

![13](https://www.dropbox.com/s/2xm0krmlw34bfpi/5-1-003.png?dl=1)
![14](https://www.dropbox.com/s/d8cois019cxe7mf/5-1-004.png?dl=1)

Finalmente comprobamos que todo está en orden:

![15](https://www.dropbox.com/s/1ezkeus9hbjgl63/5-1-005.png?dl=1)

### Ejercicio 2
Empecemos instalando qemu, para ello haremos lo siguiente:
![20](https://www.dropbox.com/s/jrlvy6dp3cl35kg/5-2-001.png?dl=1)

####Ejercicio 2.1
En este ejercicio voy a generar máquinas de ttylinux y Slitaz con Qemu de la siguiente forma:
Primero crearemos los contenedores de nuestras máquinas, para ello lo haremos como sigue:
![210](https://www.dropbox.com/s/pn3jey5iww3lrka/5-2-1-001.png?dl=1)

Repitiendo la acción para ttylinux.

Después ejecutamos lo siguiente para cada máquina:
![211](https://www.dropbox.com/s/a28pb6kosy7b2rn/5-2-1-002.png?dl=1)
![212](https://www.dropbox.com/s/e7nj1b97etcttsp/5-2-1-003.png?dl=1)

####Ejercicio 2.2
Esta parte la voy a realizar con Virtualbox. Para instalarlo me he guiado en la siguiente bibliografía:

	http://www.ubuntu-guia.com/2009/07/virtualbox-maquina-virtual-en-ubuntu.html
	http://planetadiego.com/2015/10/19/instalar-virtualbox-en-ubuntu-15-10/

Tras instalarlo, en el primer uso me ha dado un fallo propio de virtualbox, pero al reiniciar el programa se ha solucionado (después de varias ejecuciones no ha vuelto a dar indicios de error)

Aquí dejo capturas de instalación:
![220](https://www.dropbox.com/s/roo1qvu8iskhvkp/5-2-2-001.png?dl=1)
![221](https://www.dropbox.com/s/wyfagm49348nieb/5-2-2-002.png?dl=1)
![222](https://www.dropbox.com/s/7qkk4bez7p6fy3o/5-2-2-003.png?dl=1)

Una vez instalado todo ejecutamos virtualbox y procedemos a crear una VM:

![223](https://www.dropbox.com/s/1eysmgr9zqflvag/5-2-2-004.png?dl=1)

Una vez hecho seleccionamos nuestra ISO e instalamos:
![224](https://www.dropbox.com/s/3p7rq962w4hfbov/5-2-2-005.png?dl=1)
![225](https://www.dropbox.com/s/blcbx5npw8c18vf/5-2-2-006.png?dl=1)
