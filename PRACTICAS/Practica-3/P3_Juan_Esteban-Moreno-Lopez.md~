#Práctica 3. Balanceo de carga.

#En el balanceo de carga vamos a utilizar nginx y haproxy.

############################################################

##En primer lugar vamos a instalar nginx.

############################################################

##Instalamos nginx.

################################################

### Lo primero que tenemos que hacer es importar la clave del repositorio
## de software:
cd /tmp/
wget http://nginx.org/keys/nginx_signing.key
apt-key add /tmp/nginx_signing.key
rm -f /tmp/nginx_signing.key

### A continuación, debemos añadir el repositorio, editando el fichero /etc/apt/sources.list y añadiendo al final las siguientes líneas:

### con el comando nano, un editor que nos permite modificar los archivos en el
### terminal editamos el fichero  /etc/apt/sources.list
#### añadimos al final del fichero

deb http://nginx.org/packages/ubuntu/ lucid nginx" >> /etc/apt/sources.list
deb-src http://nginx.org/packages/ubuntu/ lucid nginx" >> /etc/apt/sources.list

###Obtendremos la información del fichero como podemos ver en la siguiente captura.

[![Captura edi-fic-sources](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-3/imagenes/edi-fic-sources.png)]

(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-2/imagenes/edi.fic-sources.png)

### Cuando salvemos el fichero editado actualizamos con update.

#### apt-get update

### Ahora ya podemos instalar el paquete nginx.
 
Como usuario root ejecutamos el comando

#### apt-get install nginx

### Cuando finalice la instalación obtendremos lo siguiente.

[![Captura](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-3/imagenes/final-install-nginx.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-2/imagenes/final-install-nginx.png)
################################################

## Balanceo de carga

### Con el comando nano editamos el fichero alojado en /etc/nginx/conf.d/default.conf

[![Captura](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-3/imagenes/proxy-pass.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-2/imagenes/proxy-pass.png)


####################################################################################3
















