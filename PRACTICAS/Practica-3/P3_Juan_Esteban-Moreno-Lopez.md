
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

### con el comando nano, un editor que nos permite modificar los archivos en el terminal editamos el fichero  /etc/apt/sources.list 

###Añadimos al final del fichero

deb http://nginx.org/packages/ubuntu/ lucid nginx" >> /etc/apt/sources.list
deb-src http://nginx.org/packages/ubuntu/ lucid nginx" >> /etc/apt/sources.list

###Obtendremos la información del fichero como podemos ver en la siguiente captura.

[![Captura edi-fic-sources](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-3/imagenes/edi-fic-sources-list.png)]

(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-2/imagenes/edi.fic-sources.png)

### Cuando salvemos el fichero editado actualizamos con update.

#### apt-get update

### Ahora ya podemos instalar el paquete nginx.
 
Como usuario root ejecutamos el comando

#### apt-get install nginx

### Cuando finalice la instalación obtendremos lo siguiente.

[![Captura](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-3/imagenes/final-install-nginx.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-3/imagenes/final-install-nginx.png)
################################################

## Balanceo de carga

### Con el comando nano editamos el fichero alojado en /etc/nginx/conf.d/default.conf

[![Captura](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-3/imagenes/proxy-pass.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-3/imagenes/proxy-pass.png)

####################################################################################



Para especificar a nginx que use keepalive, debemos modificar nuestro upstream añadiendo
la directiva keepalive y un tiempo de mantenimiento de la conexion en segundos:

upstream apaches {
	server 192.168.56.101;
	server 192.168.56.102;
	keapalive 3;
}


[![Captura](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-3/imagenes/curl.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-3/imagenes/curl.png)


### Reiniciamos nginx
sudo service nginx restart

[![Captura](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-3/imagenes/nginx-restart.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-3/imagenes/nginx-restart.png)



## Haproxy

#######################################################################

## Paramos ngnix para poder instalar haproxy
[![Captura](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-3/imagenes/parada-nginx.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-3/imagenes/parada-nginx.png)
##Procedemos a la instalacion de haproxy
sudo apt-get install haproxy

[![Captura](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-3/imagenes/haproxy-1.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-3/imagenes/nginx-restart.png)
#################################################


##Usamos la configuracion inicial como la siguiente:
[![Captura](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-3/imagenes/haproxy-carga-1.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-3/imagenes/haproxy-carga-1.png)

[![Captura](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-3/imagenes/haproxy-carga-2.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-3/imagenes/haproxy-carga-2.png)

##Comprobamos el funcionamiento de haproxy
### Lanzamos el funcionamiento haproxy mediante
#### sudo /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg
[![Captura](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-3/imagenes/haproxy-funcionando.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-3/imagenes/haproxy-funcionando.png)





