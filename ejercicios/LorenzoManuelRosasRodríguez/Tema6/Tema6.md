### Ejercicio 1 : Instalar chef en la máquina virtual que vayamos a usar:

Lo podemos descargar e instalar introduciendo en la terminal:
```
curl -L https://www.opscode.com/chef/install.sh | sudo bash
```
Podemos comprobar que se ha instalado con:
```
chef-solo -v
```

![instalación_chef](img1)

### Ejercicio 2: Crear una receta para instalar nginx, tu editor favorito y algún directorio y fichero que uses de forma habitual.

Para la realización del ejercicio realizaremos los siguientes pasos:

- Creación de los directorios con las recetas.

![instalación_chef](img2_1)

- Creación de los ficheros **default.rb** dentro de los directorios del anterior paso. Estos ficheros contendrán las recetas para instalar **nginx** y **nano**.

![instalación_chef](img2_2)

![instalación_chef](img2_3)

- Creación dentro del directorio **chef** de los archivos **node.json** y **solo.rb**

![instalación_chef](img2_4)

- Ejecutamos:

![instalación_chef](img2_5)

-  La jerarquía resultante del ejercicio es la siguiente:

![instalación_chef](img2_5)

### Ejercicio 3: Escribir en YAML la siguiente estructura de datos en JSON

```
{ uno: "dos",tres: [ 4, 5, "Seis", { siete: 8, nueve: [ 10, 11 ] } ] }

---
    - uno: "dos"
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

###	Ejercicio 4: Desplegar los fuentes de la aplicación de DAI o cualquier otra aplicación que se encuentre en un servidor git público en la máquina virtual Azure (o una máquina virtual local) usando ansible.

Para realizar el ejercicio realizamos los siguientes pasos:

- Instalo Ansible:

```
$ sudo pip install paramiko PyYAML jinja2 httplib2 ansible

```
- Añado la máquina de Amazon al inventario:
```
$ echo "ec2-52-11-219-71.us-west-2.compute.amazonaws.com" > ~/ansible_hosts
```
- Defino la variable de entorno que indica la localización del fichero:
```
$ export ANSIBLE_HOSTS=~/ansible_hosts
```

- Configuro ssh para la conexión con Amazon.

![img2](img2)

- El archivo **.pem** descargado debo añadirlo a la configuración ssh:

```
ssh-add "ruta-archivo-.pem"

```

- Compruebo la conexión con Ansible:
```
ansible all -u ubuntu -i ansible_hosts -m ping
```

![img3](img3)

- Instalo librerías en la máquina:
```
ansible all -u ubuntu -m command -a "sudo apt-get install python-setuptools python-dev build-essential git -y"
ansible all -u ubuntu -m command -a "sudo easy_install pip"
```

- Descargo la aplicación:
```
ansible all -u ubuntu -m git -a "repo=https://github.com/lorenmanu/prueba_dai.git  dest=~/pruebaDAI version=HEAD"
```

- Instalo los requisitos:

```
ansible all -u ubuntu -m command -a "sudo pip install -r prueba_dai/requirements.txt"

```

- Ejecuto la aplicación:


```
ansible all -u ubuntu -m command -a "sudo python prueba_dai/manage.py runserver 0.0.0.0:80"
```

- Mi aplicación con los siguientes pasos funcionando:

![img4](img4)


**Nota**: Antes deberíamos haber creado nuestra instancia en Amazon, se puede ver [aquí](https://github.com/lorenmanu/submodulo-lorenzo/blob/master/documentacion/ec2.md).
