#Tema 6

##Ejercicios

###Ejercicio 1
**Instalar chef en la máquina virtual que vayamos a usar**
1. He procedido descargándolo directamente de la página web:
~~~
curl -L https://www.opscode.com/chef/install.sh | sudo bash
~~~
![ChefLinuxMint](http://i1016.photobucket.com/albums/af281/raperaco/ChefLinuxMint_zpshvbevwah.png)


###Ejercicio 2
**Crear una receta para instalar nginx, tu editor favorito y algún directorio y fichero que uses de forma habitual.**
1. Crear los directorios para las recetas:
~~~
mkdir -p chef/cookbooks/nginx/recipes
mkdir -p chef/cookbooks/geany/recipes
~~~

2. Crear los ficheros para las recetas en su correspondiente directorio. Estos serán los ficheros **default.rb**:
- Para NGINX
En chef/cookbooks/nginx/recipes/default.rb:
~~~
package 'nginx'
~~~
    
- Para Geany
En chef/cookbooks/geany/recipes/default.rb:
~~~
package 'geany'
directory '/home/alex/Documentos/geany'
file "/home/alex/Documentos/geany/LEEME" do
	owner "alex"
    group "alex"
    mode 00644
    action :create
    content "Directorio para documentos diversos de Geany"
end
~~~

3. Crear el fichero **node.json** con las recetas a ejecutar (en mi caso lo creo en la ruta /home/alex/chef):
~~~
{
	"run_list":["recipe[nginx]", "recipe[geany]"]
}
~~~

4. En el directorio chef (en mi caso /home/alex/chef) incluimos el fichero de configuración **solo.rb** que incluye referencias a los ficheros de recetas y al fichero de recetas a ejecutar (node.json):
~~~
file_cache_path "/home/alex/chef"
cookbook_path "/home/alex/chef/cookbooks"
json_attribs "/home/alex/chef/node.json"
~~~

5. Ejecutamos chef para que lleve a cabo sus tareas (en este caso instalación de nginx, emacs y creación de directorio y fichero):
~~~
sudo chef-solo -c chef/solo.rb
~~~
![ChefSolo](http://i1016.photobucket.com/albums/af281/raperaco/ChefSolo_zpsvwdydnur.png)

6. Comprobamos el estado de nginx y la creación del fichero LEEME abriéndolo con el editor Geany:
![ChefSoloNginx](http://i1016.photobucket.com/albums/af281/raperaco/ChefSoloNginx_zps9lowtnfg.png)
![ChefSoloGeany](http://i1016.photobucket.com/albums/af281/raperaco/ChefSoloGeany_zpsh3h7sbuv.png)


###Ejercicio 3
**Escribir en YAML la siguiente estructura de datos en JSON**
~~~
{ uno: "dos",
  tres: [ 4, 5, "Seis", { siete: 8, nueve: [ 10, 11 ] } ] }
~~~

En YAML, sería:
~~~
-uno : "dos"
-tres :
	- 4
	- 5
	- "Seis"
	- 
		-siete : 8
        -nueve :
        	- 10
        	- 11
~~~


###Ejercicio 4
**Desplegar los fuentes de la aplicación de DAI o cualquier otra aplicación que se encuentre en un servidor git público en la máquina virtual Azure (o una máquina virtual local) usando ansible.**
1. Instalar Ansible:
~~~
sudo pip install paramiko PyYAML jinja2 httplib2 ansible
~~~

2. Añadir la máquina sobre la que desplegaremos la aplicación, en mi caso una máquina virtual de Azure, al fichero inventario:
~~~
echo "azurevm-ubuntu14-alex.cloudapp.net" > ~/ansible_hosts
~~~

3. Indicar la ubicación del fichero inventario mediante una variable de entorno:
~~~
export ANSIBLE_HOSTS=~/ansible_hosts
~~~