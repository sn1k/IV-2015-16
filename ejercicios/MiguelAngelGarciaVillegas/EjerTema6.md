# Asignatura: IV Grupo de Practicas Miercoles 8:30h a 10:30h
## Miguel Ángel García Villegas

# Ejercicios Tema 6

## Hay varios tutoriales que te permiten, con relativa rapidez, comenzar a trabajar con Chef-solo en un servidor; este te proporciona una serie de ficheros que puedes usar y este otro es más directo, dando una serie de órdenes. En todo caso, se trata básicamente tener acceso a un servidor o máquina virtual, instalar una serie de aplicaciones en él y ejecutarlas sobre un fichero de configuración

## Ejercicio 1.
### Instalar chef en la máquina virtual que vayamos a usar.

Una forma más rápida de instalar Chef es descargarlo directamente desde la página web.

Así que ejecutamos en el terminal: ***curl -L https://www.opscode.com/chef/install.sh | sudo bash***

Para comprobar que se ha instalado y la versión que tenemos instalada ejecutamos: ***chef-solo -v***

![Chef en ubuntu](https://www.dropbox.com/s/wlkfx0wotff4sqn/01.1.png?dl=1)

## Ejercicio 2.
### Crear una receta para instalar nginx, tu editor favorito y algún directorio y fichero que uses de forma habitual.

Vamos a crear los directorios en nuestro caso para ***nginx*** y ***nano***

Ejecutamos en el terminal ***mkdir -p chef/cookbooks/nginx/recipes***
y ***mkdir -p chef/cookbooks/nano/recipes***

Ahora en dichos directorios vamos a meter el archivo ***default.rb*** indicando en nuestro caso, para nginx.

default.rb para nginx:

    package 'nginx'
    directory "/home/magvugr/Documentos/nginx"
    file "/home/magvugr/Documentos/nginx/LEEME" do
        owner "magvugr"
        group "magvugr"
        mode 00544
        action :create
        content "Directorio para nginx"
    end

Ahora creamos el archivo ***node.json***

    {
        "run_list":["recipe[nginx]", "recipe[nano]"]
    }

Y finalmente el archivo ***solo.rb***

    file_cache_path "/home/magvugr/chef"
    cookbook_path "/home/magvugr/chef/cookbooks"
    json_attribs "/home/magvugr/chef/node.json"


Quedando nuestros archivos de la siguiente forma:

![archivos](https://www.dropbox.com/s/hgd4e1qqcyiyeeh/02.1.png?dl=1)

Ahora ejecutamos en el terminal ***sudo chef-solo -c chef/solo.rb*** para la instalación de los paquetes.

![chef-solo -c chef/solo.rb](https://www.dropbox.com/s/iogmk4anvw2ufwm/02.2.png?dl=1)
![chef-solo -c chef/solo.rb](https://www.dropbox.com/s/fw2150x6l9b3vh3/02.3.png?dl=1)

Una vez acabado, lo que hacemos es comprobar de nuevo, con el comando ***tree*** los archivos y directorios.

![archivos](https://www.dropbox.com/s/akrl4wud08ipdyl/02.4.png?dl=1)

Comprobamos que el estado de nginx y vemos que está corriendo.
![nginx is running](https://www.dropbox.com/s/qnykas8d1tptlj9/02.6.png?dl=1)

Podemos consultar los resultados

![resultados](https://www.dropbox.com/s/9ubufr9krqs82fk/02.5.png?dl=1)

Hemos añadido una receta más para geany,

Ejecutamos en el terminal ***mkdir -p chef/cookbooks/geany/recipes***

Ahora en dichos directorios vamos a meter el archivo ***default.rb*** indicando en nuestro caso, para geany.

default.rb para geany:

    package 'geany'
    directory "/home/magvugr/Documentos/geany"
    file "/home/magvugr/Documentos/geany/LEEME" do
        owner "magvugr"
        group "magvugr"
        mode 00544
        action :create
        content "Ejer2: Directorio para Geany"
    end

Ahora añadimos al archivo ***node.json***

    {
        "run_list":["recipe[nginx]", "recipe[nano]", "recipe[geany]"]
    }

Y finalmente ejecutamos:


Ahora ejecutamos en el terminal ***sudo chef-solo -c chef/solo.rb*** para la instalación de los paquetes.

![chef-solo -c chef/solo.rb](https://www.dropbox.com/s/tealpisj6mzuypw/ejer2.7.png?dl=1)
![chef-solo -c chef/solo.rb](https://www.dropbox.com/s/gjwpttag5ykwa1m/2.8.png?dl=1)

Una vez acabado, lo que hacemos es comprobar de nuevo, con el comando ***tree*** los archivos y directorios.

![archivos](https://www.dropbox.com/s/qy5xlbgslxo92br/2.9.png?dl=1)

Podemos consultar los resultados

![resultados](https://www.dropbox.com/s/6ax8kuni2yfl7pp/2.10.png?dl=1)


## Ejercicio 3.
### Escribir en YAML la siguiente estructura de datos en JSON, { uno: "dos",  tres: [ 4, 5, "Seis", { siete: 8, nueve: [ 10, 11 ] } ] }

Formato JSON
***{ "uno": "dos", "tres": [ 4 , 5 ,"Seis" ,{ "siete":8, "nueve":[10,11]}]}***


![Json to Yaml](https://www.dropbox.com/s/goyaicw50kc8t4s/Ejer3.png?dl=1)


## Ejercicio 4.
### Desplegar los fuentes de la aplicación de DAI o cualquier otra aplicación que se encuentre en un servidor git público en la máquina virtual Azure (o una máquina virtual local) usando ansible.





## Ejercicio 5.1
### Desplegar la aplicación de DAI con todos los módulos necesarios usando un playbook de Ansible.

## Ejercicio 5.2
### ¿Ansible o Chef? ¿O cualquier otro que no hemos usado aquí?.

## Ejercicio 6.
### Instalar una máquina virtual Debian usando Vagrant y conectar con ella.

Debido a diferentes pruebas, al instalar Vagrant por el terminal ejecutando el comando ***sudo apt-get install vagrant***, esto instala la versión de Vagrant 1.4.3, lo que ocurre es que se requiere para nuestra práctica una versión posterior a la 1.6. Debemos de descargar la versión que queremos e instalarla en mi caso:

Descargo [vagrant_1.8.1_x86_64.deb](https://releases.hashicorp.com/vagrant/1.8.1/vagrant_1.8.1_x86_64.deb) y lo instalo ejecutando:
***sudo dpkg -i vagrant_1.8.1_x86_64.deb***

![instalando vagrant 1.8.1](https://www.dropbox.com/s/rvwgqwkdz8p7ul7/ejer6.png?dl=1)

Ahora elegimos una distribución [Debian](http://www.vagrantbox.es/) en mi caso: ***Debian Jessie 8.0 RC2 64-bit***

Ahora instalamos la versión de debian, ejecutando en el terminal:
``vagrant box add debian http://static.gender-api.com/debian-8-jessie-rc2-x64-slim.box``

![instalando debian vagrant](https://www.dropbox.com/s/g7ms810hvmtn99t/ejer6.2.png?dl=1)

Una vez que termine vamos a ejecutar ***vagrant init debian*** ésto creará en el repositorio un archivo ***Vagrantfile***

![Vagrantfile](https://www.dropbox.com/s/yjztqcn8fgwaczx/ejer6.3.png?dl=1)

Ahora ejecutamos ***vagrant up***

![Vagrantfile](https://www.dropbox.com/s/9rtmy8eujsm1zbg/ejer6.7.png?dl=1)

Vamos a nuestro VirtualBox, y comprobamos que tenemos nuestra máquina virtual debian que acabamos de crear con vagrant.

Vamos a conectarnos con ssh, ejecutando en el terminal ***vagrant ssh*** introducimos vagrant como usuario y contraseña y entramos.

![Vagrantfile](https://www.dropbox.com/s/hy0tfdyz7mjoyi0/eje6.9.png?dl=1)

También he comprobado que si apago la máquina desde VirtualBox, y comprobamos que automáticamente nos desconecta.

![Vagrantfile](https://www.dropbox.com/s/sw9sz2dyt8kvhi8/Ejer6.10.png?dl=1)


## Ejercicio 7.
### Crear un script para provisionar `nginx` o cualquier otro servidor web que pueda ser útil para alguna otra práctica

He creado un script ningx.sh con el siguiente contenido


    #!/bin/bash
    sudo apt-get update && apt-get install -y nginx
    sudo service nginx restart && sudo service nginx status

Vamos a crear el archivo vagrant con el siguiente contenido


    # -*- mode: ruby -*-
    # vi: set ft=ruby :

    Vagrant.configure(2) do |config|
      config.vm.box = "debian"

      config.vm.provision "shell",
      	path: "nginx.sh"
    end

Después de tener los archivos ejecutamos en el terminal, ***vagrant up*** para que nos cree la máquina con el servicio
indicado en el script.

![mv creada](https://www.dropbox.com/s/fc439frzq5wyvny/Ejer7.1.png?dl=1)

## Ejercicio 8.
### Configurar tu máquina virtual usando vagrant con el provisionador ansible
