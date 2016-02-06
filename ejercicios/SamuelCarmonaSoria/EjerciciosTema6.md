# Samuel Carmona Soria
# Tema 6

## Ejercicio 1
**Instalar chef en la máquina virtual que vayamos a usar.**

kkPrimero, vamos a conectarnos a nuestra máquina virtual de Azure, primero hacemos ```azure login``` y tras ello, arrancamos la máquina y nos conectamos por ssh, como se ve en la imagen siguiente:
![Acceso SSH a máquina virtual en Azure](http://i.cubeupload.com/6JnC1a.jpg)

Una vez en la máquina, tal como se explica [aquí](http://gettingstartedwithchef.com/first-steps-with-chef.html), una manera fácil de instalar chef es ejecutando la siguiente orden:
```
curl -L https://www.opscode.com/chef/install.sh | sudo bash
```
Éste comando se descargará el script para la instalación de **chef-solo**, que consiste en una versión aislada que permite trabajar en una máquina desde la misma.

![Instalando CHEF](http://i.cubeupload.com/BWafQT.jpg)

Con `chef-solo -v` comprobamos que está instalado, y nos muestra la versión instalada:
![Versión chef-solo](http://i.cubeupload.com/fhJk0O.jpg)
