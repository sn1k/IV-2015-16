#Ejercicios - Jesús Prieto López
##TEMA 6

###Ejercicio 1: Instalar chef en la máquina virtual que vayamos a usar.

Voy a utilizar una máquina virtual que tenía creada con VMware Workstation. La máquina virtual tiene el SO Ubuntu Server 14.04 de 64 bits.

Podemos instalar **chef** con la siguiente orden:

`$ curl -L https://www.opscode.com/chef/install.sh | sudo bash`

Para comprobar que se ha instalado correctamente:

`$ chef-solo -v`

![Instalación de chef y versión instalada](cap1)

###Ejercicio 2: Crear una receta para instalar nginx, tu editor favorito y algún directorio y fichero que uses de forma habitual.

Creamos las recetas para instalar **nginx** y el editor seleccionado, en este caso **gedit**. 

Preparamos los directorios necesarios para poder utilizar las recetas creadas para **chef**. Lo principal será un directorio llamado *chef* del que colgará un directorio *cookbooks* y este a su vez tendrá tantos directorios como recetas hagamos. Dentro de cada directorio de la receta deberá haber un directorio llamado *recipes*. Tal que así

	chef/cookbooks/nginx/recipes
	chef/cookbooks/gedit/recipes

Necesitamos configurar un archivo para cada uno que actuará como receta. Este archivo deberá indicarse con el nombre de **default.rb**.

- Receta nginx

```ruby
package 'nginx'
directory '/home/jes/PruebaRecetas/nginx'
file '/home/jes/PruebaRecetas/nginx/LEEME' do
	owner 'jes'
	group 'jes'
	mode 00544
	action :create
	content 'Directorio de nginx creado por receta'
end
```

- Receta gedit

```ruby
package 'gedit'
directory '/home/jes/PruebaRecetas/gedit'
file '/home/jes/PruebaRecetas/gedit/LEEME' do
	owner 'jes'
	group 'jes'
	mode 00544
	action :create
	content 'Directorio de gedit creado por receta'
end
```

Estos dos archivos, deberá ir cada uno en su carpeta correspondiente dentro de *recipes*.

Tenemos que crear ahora el fichero que indica las recetas que deseamos que se ejecuten. Este archivo deberá llamarse **node.json** y lo crearemos en el directorio *chef*. Al querer ejecutar las recetas creadas anteriores el archivo quedaría:

```
{
	"run_list":[ "recipe[nginx]", "recipe[gedit]"]
}
```

El archivo encargado de indicar las referencias a los archivos anteriores será **solo.rb**, teniendo que indicar el camino a los mismos para poder lanzarlos.

```ruby
file_cache_path "/home/jes/chef"
cookbook_path "/home/jes/chef/cookbooks"
json_attribs "/home/jes/chef/node.json"
```

Una vez hecho todo esto, podemos proceder a ejecutar nuestras recetas y comprobar el funcionamiento.

`$ chef-solo -c solo.rb`

![Ejecución de las recetas de chef](cap2)

###Ejercicio 3: Escribir en YAML la siguiente estructura de datos en JSON
`{ uno: "dos",  tres: [ 4, 5, "Seis", { siete: 8, nueve: [ 10, 11 ] } ] }`

Correspondiente en YAML:

```
---
- uno: "dos"
- tres:
	- 4
	- 5
	- "Seis"
	-
		- siete: 8
		- nueve:
			- 10
			- 11
```






