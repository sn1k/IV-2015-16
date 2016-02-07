Ejercicio 1 .
-------
* Instalamos chef:
![Imagen 1.1](https://www.dropbox.com/s/cwc4tqfza3oldsg/1.1.png?dl=1)
 

Ejercicio 2 .
-------
* Creamos los directorios:
![Imagen 2.1](https://www.dropbox.com/s/cwc4tqfza3oldsg/1.1.png?dl=1)

* Creamos el archivo *solo.rb* dentro de la carpeta chef:
![Imagen 2.2](https://www.dropbox.com/s/cwc4tqfza3oldsg/1.1.png?dl=1)

* Creamos el archivo *default.rb* tanto de nginx como del editor gedit dentro de la carpeta chef:
![Imagen 2.3](https://www.dropbox.com/s/cwc4tqfza3oldsg/1.1.png?dl=1)

![Imagen 2.4](https://www.dropbox.com/s/cwc4tqfza3oldsg/1.1.png?dl=1)

* Creamos el archivo *node.json* dentro de la carpeta chef:
![Imagen 2.5](https://www.dropbox.com/s/cwc4tqfza3oldsg/1.1.png?dl=1)

* Ejecutamos y observamos que todo se instala:
![Imagen 2.6](https://www.dropbox.com/s/cwc4tqfza3oldsg/1.1.png?dl=1)

Ejercicio 3 .
-------
~~~
--- 
- 
  tres: 
    - 4
    - 5
    - seis
    - 
      - 
        siete: 8
      - "nueve:[10,11]"
  uno: dos
~~~


Ejercicio 6 .
-------
* Instalamos vagrant:
![Imagen 2.1](https://www.dropbox.com/s/cwc4tqfza3oldsg/1.1.png?dl=1)

* Creamos la máquina con Debian:
![Imagen 2.2](https://www.dropbox.com/s/cwc4tqfza3oldsg/1.1.png?dl=1)

* Para inicializar la máquina virtual usaremos * vagrant up*.

* Para conectarnos usaremos *vagrant ssh*.
