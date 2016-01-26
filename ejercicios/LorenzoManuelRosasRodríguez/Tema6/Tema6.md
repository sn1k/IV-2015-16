### Ejercicio 1 : Instalar chef en la máquina virtual que vayamos a usar:

Lo podemos descargar e instalar introduciendo en la terminal:
```
curl -L https://www.opscode.com/chef/install.sh | sudo bash
```

![instalación_chef](img1_1)

Podemos comprobar que se ha instalado con:
```
chef-solo -v
```

![instalación_chef](img1_2)

**Nota**: ubuntu ya me permitía instalarlo usando **apt**:

```

sudo apt-get install chef

```

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


### Ejercicio 5:
### 1.Desplegar la aplicación de DAI con todos los módulos necesarios usando un playbook de Ansible.


### 2.¿Ansible o Chef? ¿O cualquier otro que no hemos usado aquí?.


### Ejercicio 6:Instalar una máquina virtual Debian usando Vagrant y conectar con ella.




### Ejercicio 7: Crear un script para provisionar `nginx` o cualquier otro servidor web que pueda ser útil para alguna otra práctica


### Ejercicio 8: Configurar tu máquina virtual usando vagrant con el provisionador ansible.
