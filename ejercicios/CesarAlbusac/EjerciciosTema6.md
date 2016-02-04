##Ejercicio 1:Instalar chef en la máquina virtual que vayamos a usar

Para instalarlo, ejecutamos la siguiente orden en la consola:
```curl -L https://www.opscode.com/chef/install.sh | bash``` 

![Ejercicio1_1](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio1_zpsgjsubtc9.png)

![Ejercicio1_2](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio1_2_zpsm87pp6mt.png)


##Ejercicio 2:Crear una receta para instalar nginx, tu editor favorito y algún directorio y fichero que uses de forma habitual.

En primer lugar, tenemos que crear los directorios para las recetas. Escribimos lo siguiente en el terminal:
```
mkdir -p chef/cookbooks/nginx/recipes
mkdir -p chef/cookbooks/nano/recipes
```

Ahora, tenemos que crear los ficheros de recetas para nginx y nano. Se llaman default.rb y se ubicarán en los directorios
anteriores.

Contenido de default.rb para nginx:

![nginx](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio2_nginx_zpssmrwvpoe.png)

Contenido de default.rb para nano:

![nano](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio2_nano_zpska4muyx0.png)

Ahora tenemos que crear el archivo node.json con el siguiente contenido:
```
{
      "run_list":["recipe[nginx]", "recipe[nano]"]
}
```

En la carpeta chef, tenemos que crear el archivo solo.rb, con el siguiente contenido:
```
file_cache_path "/home/cesar/chef" 
cookbook_path "/home/cesar/chef/cookbooks" 
json_attribs "/home/cesarj/chef/node.json" 
```

Finalmente instalamos los paquetes ejecutando la orden ```sudo chef-solo -c chef/solo.rb```:
![Ejercicio2_3](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio2_3_zpsrq43anx0.png)

![Ejercicio2_4](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio2_4_zpsl5dow3zg.png)

Podemos ver que se ha realizado correctamente.Nginx está corriendo:
![Ejercicio2_5](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio2_5_zpsaol525tt.png)

Y los archivos LEEME se han creado correctamente:
![Ejercicio2_6](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio2_6_zpsi301moq1.png)




##Ejercicio 3:Escribir en YAML la siguiente estructura de datos en JSON
{ uno: "dos", tres: [ 4, 5, "Seis", { siete: 8, nueve: [ 10, 11 ] } ] }

La estructura en YAML sería la siguiente:
```
---
    uno: "dos"
    tres: 
        - 4
        - 5
        - "Seis"
        - 
            siete: 8
            nueve: 
                - 10
                - 11

```

##Ejercicio 4: Desplegar los fuentes de la aplicación de DAI o cualquier otra aplicación que se encuentre en un servidor git público en la máquina virtual Azure (o una máquina virtual local) usando ansible.

Antes de nada, tenemos que instalar Ansible. El comando que tenemos que escribir en el terminal es:
```sudo pip install paramiko PyYAML jinja2 httplib2 ansible```

Me ha dado algunos problemas, ya que no me creaba la carpeta de ansible en /etc. Así que he instalado
de nuevo Ansible, con el comando ```sudo apt-get install ansible```. Y de esta manera ya crea el directorio
correspondiente en la carpeta /etc/.

Una vez hecho ésto, ahora tenemos que crear el inventario añadiendo nuestra máquina virtual de azure mediante la
orden ```echo "maquina-cesar-ubu5.cloudapp.net" > ~/ansible_hosts ```
Definimos la variable de entorno para que Ansible sepa donde se encuentra el fichero:
```export ANSIBLE_HOSTS=~/ansible_hosts```:
![Ejercicio4_1](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio4_zpsgfyr7b9v.png)

También he editado el archivo /etc/ansible/hosts añadiendo **maquina-cesar-ubu5.cloudapp.net** , de lo contrario me 
daba problemas.


Ahora, iniciamos sesión en Azure como hicimos en algunos ejercicios del tema anterior, con ```azure login```, y una
vez que ya estemos logeados, arrancamos la máquina virtual que teníamos creada, mediante el comando
```azure vm start maquina-cesar-ubu5``` :
![Ejercicio4_2](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio4_2_zpspbanmdie.png)



Ahora, pasamos a configurar el ssh para poder acceder a la máquina virtual.
Creamos una pareja de llaves pública/privada con ```ssh-keygen -t dsa ```.
Una vez que se haya creado correctamente,la copiamos a nuestra máquina virtual en azure mediante el comando ```ssh-copy-id -i .ssh/id_dsa.pub cesar@maquina-cesar-ubu5.cloudapp.net```:
![Ejercicio4_3](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio4_3_zpsnpi8czxu.png)

Ahora podemos ver que podemos acceder a la máquina sin autiticarnos:
![Ejercicio4_4](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio4_4_zpslh5octyj.png)


Ahora, probamos que hay conexión con ansible mediante el comando ```ansible all -u cesar -i ansible_hosts -m ping```:
![Ejercicio4_5](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio4_5_zpsx7gkmek1.png)


Ahora, tenemos que instalar las dependencias necesarias. Lo hacemos con los siguientes comandos:
``` ansible all -u cesar -m command -a "sudo apt-get install python-setuptools python-dev build-essential git -y"```:
![Ejercicio4_6_2](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio4_6_2_zpskuy8rpau.png)

```ansible all -u cesar -m command -a "sudo easy_install pip"```:
![Ejercicio4_7](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio4_7_zpsfcxq7loj.png)


Ahora, nos tenemos que descargar las aplicación de github e instalar los requirements.
Para descargar nuestra aplicación, ejecutamos lo siguiente:
```ansible all -u cesar -m git -a "repo=https://github.com/cesar2/DAI-BARES.git  dest=~/DAIprueba version=HEAD"```:
![Ejercicio4_9](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio4_9_zps6k0a32sb.png)

Instalar requirements: ```ansible all -u cesar -m command -a "sudo pip install -r pruebaDAI/requirements.txt"```:
![Ejercicio4_10](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio4_10_zpspds4kg2v.png)

Dentro de la máquina de azure, comprobamos que están todos los archivos que hemos puesto desde github:
![Ejercicio4_11](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/078fb8c1-656a-4a3c-81a0-a44a6dacfe94_zpsvsbfhtr8.png)

**Importante: Antes de ejecutar nuestra aplicación, debemos comprobar que nginx no se está ejecutando en la máquina virtual**

**También podemos tener algún problema con la liberación del puerto 80. Si tenemos que liberarlo, ejecutamos en la consola** ```ansible all -u cesar -m command -a "sudo fuser -k 80/tcp"```.

Para abrir el tráfico en azure(en caso de que no lo esté): ```azure vm endpoint create maquina-cesar-ubu5 80 80```

Ahora, para ejecutar la aplicación, escribimos ```ansible all -u cesar -m command -a "sudo python pruebaDAI/manage.py runserver 0.0.0.0:80"```:
![Ejercicio4_14](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio4_14_zpsistejdxb.png)

Ahora vamos a la dirección de nuestra máquina y podemos ver que está funcionando correctamente.
Escribimos en el navegador **maquina-cesar-ubu5.cloudapp.net/rango/**:
![Ejercicio4_12](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio4_12_zpsk595finc.png)

Por último, apagamos la máquina virtual con ```azure vm shutdown maquina-cesar-ubu5```.


##Ejercicio 5:
###1.Desplegar la aplicación de DAI con todos los módulos necesarios usando un playbook de Ansible.

En primer lugar, para definir el host, debemos editar algunos archivos, como muestro a continuación:
En el archivo que teníamos creado antes, debemos editarlo para dejarlo así:
![Ej5_ans](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio5_ansiblehost_zpszpfnfecz.png)

También he editado el archivo **/etc/ansible/hosts** de la misma manera. Queda tal que así:
![Ej5_etc](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio5_etcansible_zpsntiq6yr8.png)

Y por último, tenemos que crear el archivo **.yml**, que en mi caso se va a llamar **appansible.yml**. Contendrá
la siguiente información:
![Ej5_yml](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio5_appansible_zpsdjse1mlm.png)

**Atención. Al igual que anteriormente, debemos comprobar el estado de nginx, y en caso de que se esté ejecutando, lo detenemos**

Ejecutamos el archivo **.yml** con la orden ```ansible-playbook -u cesar appansible.yml```:
![Ejercicio5_1](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio5_zpsiidivd1p.png)

Y ahora abrimos el navegador y vamos a la dirección **http://maquina-cesar-ubu5.cloudapp.net/rango/**:
![Ejercicio5_2](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio5_2_zpstxa4dvot.png)

Por último, apagamos la máquina virtual con ```azure vm shutdown maquina-cesar-ubu5```.


###2.¿Ansible o Chef? ¿O cualquier otro que no hemos usado aquí?.
Ansible, ya que lo veo más sencillo y nos da la posibilidad de realizar las tareas sin estar en el servidor.

##Ejercicio 6:Instalar una máquina virtual Debian usando Vagrant y conectar con ella.

Antes de nada, tenemos que instalar valgran con la orden ```sudo apt-get install valgran```:

Ahora, descargamos la máquina virtual que deseemos instalar:
```vagrant box add debian https://github.com/holms/vagrant-jessie-box/releases/download/Jessie-v0.1/Debian-jessie-amd64-net boot.box ```
![Ejercicio6](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio6_zpsqwwozl4p.png)

Ahora, como dice en la tería, cramos un fichero Vagranfile con ```vagrant init debian```.
![Ejercicio6_2](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio6_2_zpsqdmhdquz.png)

Inicializamos la máquina con ```vagrant up```:
![Ejercicio6_3](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio6_3_zpsecpngcx9.png)

Y ya se puede empezar a trabar con ella con ```vagrant ssh```:
![Ejercicio6_4](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio6_4_zpsorutramg.png)

##Ejercicio 7:Crear un script para provisionar `nginx` o cualquier otro servidor web que pueda ser útil para alguna otra práctica.

Para provisionar nginx, tenemos que crear un archivo parecido al que hay en la teoría:
```
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
	config.vm.box = "centos65"

    config.vm.provision "shell",
		inline: "yum install -y emacs"
end
```
Pero poniendo en config.vm.box el nombre de nuestra máquina que hemos creado, y en inline, la orden necesaria para
poder instalar nginx, en este caso, ```sudo apg-get install -y nginx && sudo service nginx start```.

Así, vamos al directorio en que anteriormente creamos el archivo Vagrantfile, que no contendrá órdenes a ejecutar aún, 
aunque sí otras lineas como el nombre de la máquina. Al editarlo, nos debe quedar algo así:
![Ejercicio7](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio7_zpsmconluum.png)

Ejecutamos con ```vagran provision```:
![Ejercicio7_2](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio7_2_zpszajmww7d.png)

Ahora, nos conectamos a la máquina mediante ssh y comprobamos que el servicio nginx está funcionando:
![Ejercicio7_3](http://i1155.photobucket.com/albums/p543/cesypozo/Ejercicios%20tema%206/ejercicio7_3_zps201npm4o.png)

##Ejercicio 8: Configurar tu máquina virtual usando vagrant con el provisionador ansible



