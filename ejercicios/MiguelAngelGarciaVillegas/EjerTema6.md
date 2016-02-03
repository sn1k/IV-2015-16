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

Vamos a empezar a escribir una recetilla del Chef. Generalmente, escribir una receta es algo más complicado, pero comenzaremos por una receta muy simple que instale el imprescindible emacs y le asigne un nombre al nodo.

Creamos el directorio chef en algún sitio conveniente y dentro de ese directorio irán diferentes ficheros.

El fichero que contendrá efectivamente la receta se llamará default.rb

El nombre del fichero indica que se trata de la receta por omisión, pero el nombre de la receta viene determinado por el directorio en el que se meta, que podemos crear de un tirón con ***mkdir -p chef/cookbooks/emacs/recipes***
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

Resultados

![resutados](https://www.dropbox.com/s/9ubufr9krqs82fk/02.5.png?dl=1)




## Ejercicio 3.
### Escribir en YAML la siguiente estructura de datos en JSON, { uno: "dos",  tres: [ 4, 5, "Seis", { siete: 8, nueve: [ 10, 11 ] } ] }

## Ejercicio 4.
### Desplegar los fuentes de la aplicación de DAI o cualquier otra aplicación que se encuentre en un servidor git público en la máquina virtual Azure (o una máquina virtual local) usando ansible.

## Ejercicio 5.1
### Desplegar la aplicación de DAI con todos los módulos necesarios usando un playbook de Ansible.

## Ejercicio 5.2
### ¿Ansible o Chef? ¿O cualquier otro que no hemos usado aquí?.

## Ejercicio 6.
### Instalar una máquina virtual Debian usando Vagrant y conectar con ella.

## Ejercicio 7.
### Crear un script para provisionar `nginx` o cualquier otro servidor web que pueda ser útil para alguna otra práctica

## Ejercicio 8.
### Configurar tu máquina virtual usando vagrant con el provisionador ansible
