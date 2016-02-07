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

Dentro de la carpeta chef creamos node.json y solo.rb. Dentro del primer primero indicamos lo que queremos instalar y en el segundo las referencias a los archivos (instalables):

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

Para este ejercicio usaré la máquina virtual que tenía del tema anterior. A parte de explicar los pasos para hacer el ejercicio mostraré algunos errores que van saliendo para que podamos apreciar la mejora en hacerlo con un archivo de provisionamiento con ansible en el siguiente ejercicio.

Primero instalamos Ansible:
```
sudo pip install paramiko PyYAML jinja2 httplib2 ansible
```
Ahora incluimos la máquina de Azure al inventario de ansible y defininimos la variable de entorno

![ansible1](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_018_zpsye6twgaf.png)

Ahora hacemos ```azure login``` para conectarnos a la cuenta de azure (ya explicado en el tema antrior, copiar enlace y ponerle el código).
Y iniciamos la máquina con con ```azure vm start maquina-ubuntu-pmmre```

Ansible funciona conectándose con ssh por eso para usarlo deberemos pasarle a la nueva máquina la llave publica de la máquina que estamos usando, en mi caso es Koding.
Si no tenemos generadas las llaves las generamos con ```ssh-keygen -t dsa ``` y las enviamos a la máquina con la siguiente orden:
```
ssh-copy-id -i .ssh/id_dsa.pub pablo@maquina-ubuntu-pmmre.cloudapp.net
```

Comprobamos que podemos hacer un ssh y que ahora no nos pide la clave:
![ansibleSSH](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_019_zpsqrbgytb3.png)


Y comprobamos con Ansible que podemos conectarnos bien mediante un ping:
![ansiblePing](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_020_zps9cgdswdn.png)

Nos descargamos con ansible nuestro proyecto usando git:
![ansibleGit](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_022_zpsnvsmwmo0.png)

Vamos a instalar los paquete con pip pero nos dice que no se encuentra:
![](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_023_zps2j1c15yx.png)

Actualizamos los repositorios:
![](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_024_zpsjrmxsgt6.png)

Instalamos pip:
![](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_025_zpsz7yo6zts.png)

Nos sale el siguiente error al instentar instalar de nuevo con pip:
![](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_027_zpswklgbcdq.png)

Así que ahora sabemos que nos faltan los siguientes paquetes que los instalamos:
![](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_026_zpsgrc3j0ye.png)

![](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_028_zpsthfcpoqm.png)

![](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_029_zpszngrjhbq.png)

![](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_030_zpsub2vgrvw.png)

![](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_031_zpsqmfrciie.png)

![](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_032_zps8hkwtb2e.png)

![](http://i393.photobucket.com/albums/pp14/pmmre/IVEjercicios5y6/IVEjercicios6/IVEjercicios6/Seleccioacuten_033_zps2fqtuxap.png)




## Ejercicio 5

### 1. Desplegar la aplicación de DAI con todos los módulos necesarios usando un playbook de Ansible.

### 2. ¿Ansible o Chef? ¿O cualquier otro que no hemos usado aquí?.

## Ejericicio 6. Instalar una máquina virtual Debian usando Vagrant y conectar con ella.

## Ejericicio 7. Crear un script para provisionar `nginx` o cualquier otro servidor
web que pueda ser útil para alguna otra práctica

## Ejercicio 8. Configurar tu máquina virtual usando vagrant con el provisionador
ansible