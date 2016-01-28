#Ejercicio 1

Para instalar Cheff, nos iremos a [su página de getting started](http://gettingstartedwithchef.com/first-steps-with-chef.html), y seguiremos la órden que se indica:

	 curl -L https://www.opscode.com/chef/install.sh | sudo bash
    
De esta forma se descargará un script que acto seguido, ejecutará. Dicho script es la instalación propia de cheff solo.

En el momento de realización de éste ejercicio, parece que la descarga del scriptinstala una versión ya obsoleta de cheff, donde nos advierte que se actualizará solo y sin dejar advertencia.

![](Ejercicio1)

#Ejercicio 2

PRimero, crearemos los directorios (dentro de la máquina virtual):
	
    mkdir -p chef/cookbooks/nginx/recipes
	mkdir -p chef/cookbooks/nano/recipes
 
Después de crear los directorios, debemos navegar hacia ellos, e incluir en cada uno, el fichero **default.rb ** correspondiente:

	cd chef/cookbooks/
- Para nginx 
```
cd nginx/recipes
vim default.rb
``` 
Y escribimos el siguiente contenido:
```
package 'nginx'
directory "/home/joseantonio/Documentos/nginx"
file "/home/joseantonio/Documentos/nginx/LEEME" do
    owner "joseantonio"
    group "joseantonio"
    mode 00544
    action :create
    content "Directorio para nginx"
end
```
- Para nano:
```
cd nano/recipes
vim default.rb
```
Y escribimos el siguiente contenido:
```
package 'nano'
directory "/home/joseantonio/Documentos/nano"
file "/home/joseantonio/Documentos/nano/LEEME" do
    owner "joseantonio"
    group "joseantonio"
    mode 00544
    action :create
    content "Directorio para nano"
end
```

sdfa
    