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



## Ejercicio 2
**Crear una receta para instalar nginx, tu editor favorito y algún directorio y fichero que uses de forma habitual.**

Antes de todo, creamos los directorios donde irán las recetas para instalar nginx y el editor que más uso, nano:

Desde el directorio /home/samu:

- ```mkdir -p chef/cookbooks/nginx/recipes```
- ```mkdir -p chef/cookbooks/nano/recipes```

Ahora, vamos a configurar los ficheros que contendrán las recetas para instalar "nginx" y "nano".

Para la configuración podemos seguir [este tutorial](http://www.mechanicalfish.net/configure-a-server-with-chef-solo-in-five-minutes/), donde explica como cofigurar un servidor con chef-solo en 5 minutos.

El fichero que contendrá la receta de instalación se llamará "default.rb", que existirá uno en cada uno de los directorios creados anteriormente (chef/cookbooks/nginx/recipes y chef/cookbooks/nano/recipes).

- Archivo receta **default.rb** para nginx:

```
package 'nginx'
directory "/home/samu/Documentos/nginx"
file "/home/samu/Documentos/nginx/LEEME" do
	owner "samu"
	group "samu"
	mode 00544
	action :create
	content "Directorio para nginx"
end
```

- Archivo receta **default.rb** para nano:

```
package 'nano'
directory "/home/samu/Documentos/nano"
file "/home/samu/Documentos/nano/LEEME" do
	owner "samu"
	group "samu"
	mode 00544
	action :create
	content "Directorio para nano"
end
```

El contenido que hemos introducido en ambos de dichos archivos, contiene ordenes que  instalarán el paquete especificado.
Creará un directorio para documentos y dentro de él un fichero que explica de qué se trata.

Antes de seguir hacia adelante, deberemos asegurarnos de que la carpeta "Documentos" y las subcarpetas "nano" y "nginx" están creadas:
```
  mkdir -p Documentos/nano
  mkdir -p Documentos/nginx
```

El siguient paso es crear un fichero llamado "node.json", que irá en el directorio "chef" y va a tener la lista de recetas a ejecutar.

- **node.json**:

```
{
        "run_list":["recipe[nginx]", "recipe[nano]"]
}
```

También vamos a crear el archivo de configuración "solo.rb", que incluirá referencias a los ficheros creados previamente.
Al igual que "node.json", éste también se guardará en el directorio chef.

- **solo.rb**:

```
file_cache_path "/home/samu/chef"
cookbook_path "/home/samu/chef/cookbooks"
json_attribs "/home/samu/chef/node.json"
```

Si queremos ver la estructura del directorio Chef podemos instlar "tree" con:
```
sudo apt-get install tree
```
Tras instalarlo ejecutamos `tree chef` y nos mostrará la estructura de directorios Chef:
![tree chef](http://i.cubeupload.com/bomW6u.jpg)

El último paso es llevar acabo la configuración isntalada, y comprobar que los paquetes  "nano" y "nginx" se instalan con la siguiente orden:
```
sudo chef-solo -c chef/solo.rb
```
Y obtendremos la siguiente salida
![demostración chef](http://i.cubeupload.com/wActlG.jpg)

Podemos ver que como ya indica, nginx y nano ya están instalados antes de la realización del ejercicio. En caso de no estarlo, se instalarían al ejecutar éste comando.
