# Gestión de configuraciones

## Ejercicio 1. Instalar chef en la máquina virtual que vayamos a usar
Para este ejercicio he creado una máquina de virtualBox.

Lo instalamos con el siguiente comando:

![instalacionChef1](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_001_zpsso5kl8kh.png)

![instalacionChef2](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_002_zpsak4hpszv.png)

Y comprovamos la versión:

![versionChef](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_003_zps1fjdfxsh.png)

## Ejericicio 2. Crear una receta para instalar nginx, tu editor favorito y algún directorio y fichero que uses de forma habitual.
Chef necesita una estructira jerarquizada de directorios para funcionar, en mi caso instalaré geany y nginx. Y lo primero es crear los directorios:
```
mkdir -p chef/cookbooks/nginx/recipes
mkdir -p chef/cookbooks/geany/recipes
```

Una vez creados nos disponemos a crear las recetas de geany y nginx que es un archivo default.rb creado cada uno dentro de su directorio. En la siguiente imagen se ve su contendio y si nos fijamos entenderemos algo mejor su estructura (fijarse en la ruta cat).

![recipes](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_063_zpsjicaomm7.png)

Dentro de la carpeta chef creamos node.json y solo.rb. Dentro del primer primero indicamos lo que queremos intstalar y en el segundo las referencias a los archivos (instalables):

![make_chef](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_064_zps2nbkhzhf.png)

Para emprezar con la instalación ejecutamos el siguiente comando ```sudo chef-solo -c chef/solo.rb``` y vemos cómo se instala todo correctamente:

![Ejecución_chef1](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_005_zpstp2qpalw.png)

![Ejecución_chef2](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_004_zpsnn5db7cc.png)

Y aqui tenemos la la estructura de directorios y lo que se ha creado dentro de Documentos:

![struct1](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_006_zpsq3igpy9v.png)

![struct2](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_065_zps6krjuoeu.png)

## Ejercicio 3. Escribir en YAML la siguiente estructura de datos en JSON
```
---
-uno:"dos"
 tres:
	- 4
	- 5
	- "Seis"
	-
		- siete: 8
		  nueve:
			- 10
			- 11
```
## Ejericicio 4. Desplegar los fuentes de la aplicación de DAI o cualquier otra aplicación que se encuentre en un servidor git público en la máquina virtual Azure (o una máquina virtual local) usando ansible.

## Ejercicio 5

### 1. Desplegar la aplicación de DAI con todos los módulos necesarios usando un playbook de Ansible.

### 2. ¿Ansible o Chef? ¿O cualquier otro que no hemos usado aquí?.

## Ejericicio 6. Instalar una máquina virtual Debian usando Vagrant y conectar con ella.

## Ejericicio 7. Crear un script para provisionar `nginx` o cualquier otro servidor
web que pueda ser útil para alguna otra práctica

## Ejercicio 8. Configurar tu máquina virtual usando vagrant con el provisionador
ansible