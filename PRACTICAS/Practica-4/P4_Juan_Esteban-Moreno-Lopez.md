#Práctica 4. Comprobar el rendimiento de servidores web
#####
##Instalamos Apache Benchmark 
sudo apt-get install apache2-utils

[![Captura Install_ab](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/Install_ab.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/Install_ab.png)
##Cuando finalice la instalación obtendremos un resultado parecido al siguiente:
[![Captura Final_Install_ab](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/fin-install-ab.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/fin-install-ab.png)
## Comprobamos el funcionamiento del apache berksmark
#### Para ello creamos un fichero que nos permita hacer peticiones al servidor, en mi caso utilizo un fichero php.
#### Su contenido es el siguiente:
[![Captura Fichero_php](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/fichero-php.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/fichero-php.png)

#Comprobar el rendimiento de servidores web con Apache Benchmark
### Lanzamos el programa con el siguiente comando:
 
ab -n 1000 -c 10 http://192.168.56.101/fichero.php

### Obtendremos un resultado parecido al siguiente:
[![Captura ab-1](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/ab-1.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/ab-1.png)
######################################################
[![Captura ab-cap](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/ab-cap.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/ab-cap.png)
###########################################################
### Ejecutamos el programa ab para el balanceador con nginx.
ab -n 1000 -c 10 http://192.168.56.103
################################################################
### Obtenemos el siguiente resultado:
[![Captura ab-cap-balanceador](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/ab-cap-balanceador-1.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/ab-cap-balanceador-1.png)
##############################################################
### Para poder ejecutar el balanceador con haproxy
######################################################
### Ejecutamos los siguientes comandos:
service nginx stop
######################################
/usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg
###############################################
### Ejecutamos el programa ab para el balanceador con haproxy.
ab -n 1000 -c 10 htttp://192.168.56.103
### Obtenemos el siguiente resultado:
[![Captura ab-balanceador-haproxy](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/ab-balanceador-haproxy.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/ab-balanceador-haproxy.png)
### Realizamos un total de 10 pruebas.
### Obtenemos la siguiente tabla con la media y la desviación estándar.
[![Captura maq1-ab](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/maq1-ab.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/maq1-ab.png)
##########################################################
### Realizamos un total de 10 pruebas donde calculamos media y la desviación estándar balanceador configuración nginx.
[![Captura balan-ab-nginx.png](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/balan-ab-nginx.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/balan-ab-nginx.png)

### Realizamos un total de 10 pruebas donde calculamos media y la desviación estándar balanceador configuración haproxy.
[![Captura balan-ab-haproxy.png](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/balan-ab-haproxy.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/balan-ab-haproxy.png)
### Para la media obtenemos:
[![Captura ab-graf-media](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/ab-graf-media.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/ab-graf-media.png)

##############################################################
#Comprobamos el rendimiento con Siege
### Instalamos Siege:
sudo apt-get install siege
##################################
### Ejecutamos el programa siege para una máquina sola con el comando:
./siege -b -t60s -v http://192.168.56.101
######################################
### Obtenemos el siguiente resultado:
[![Captura sige-cap-1](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/siege-cap-1.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/siege-cap-1.png)
########################################
### Ejecutamos el programa siege, balanceador con nginx.
./siege -b -t60s -v http://192.168.56.103
###################################################
### Obtenemos el siguiente resultado:
[![Captura siege-cap-1-balanceador](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/siege-cap-1.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/siege-cap-1-balanceador.png)
###################################################
### Ejecutamos el programa siege, balanceador con haproxy.
#########################################################
### Obtenemos el siguiente resultado:
[![Captura siege-haproxy-balanceador](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/siege-haproxy-balanceador.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/siege-haproxy-balanceador.png)
#############################################################
### Realizamos un total de 10 pruebas donde calculamos media y la desviación estándar máquina 1.
[![Captura maq1-siege](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/maq1-siege.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/maq1-siege.png)

### Realizamos un total de 10 pruebas donde calculamos media y la desviación estándar balanceador configuración nginx.
[![Captura balan-nginx](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/balan-siege-nginx.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/balan-siege-nginx.png)

### Realizamos un total de 10 pruebas donde calculamos media y la desviación estándar balanceador configuración haproxy.
[![Captura balan-haproxy](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/balan-siege-haproxy.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/balan-siege-haproxy.png)

### Para la media obtenemos la siguiente gráfica:
[![Captura siege-graf-media](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/siege-graf-media.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/siege-graf-media.png)



### Con los resultados obtenidos podemos concluir que la configuración con un balanceador haproxy obtenemos mejores resultados.
#############################################################
#Comprobamos el rendimiento con Jmeter
### Utilizamos una tercera herramienta para medir el rendimiento de servidores.
### Se trata de la herramienta Jmeter.
########################################################
### Procedemos a su instalación con el comando.
sudo apt-get install jmeter
#######################################################
### Instalación.
[![Captura install-jmeter](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/install-jmeter.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/install-jmeter.png)

###########################################################

##### Fin Instalación.

[![Captura fin-install-jmeter](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/fin-install-jmeter.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/fin-install-jmeter.png)

############################################################
### Comprobamos que se ha instalado correctamente.
#################################################
[![Captura comp-instalacion-jmeter](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/comp-instalacion-jmeter.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/comp-instalacion-jmeter.png)
##############################################
### Iniciamos el programa con el comando:
jmeter
### Iniciamos la interfaz gráfica:
##########################################
[![Captura inicio-jmeter](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/inicio-jmeter.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/inicio-jmeter.png)
###Nos vamos a Plan de Pruebas.
#### Botón derecho del ratón añadir - Hilos(Usuarios) - Grupo de hilos
[![Captura jmeter-grup-hilos](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/jmeter-grup-hilos.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/jmeter-grup-hilos.png)
#### Una vez creado el grupo de hilos, sobre el Grupo de Hilos botón derecho
#### del ratón añadir, muestreador- petición http
[![Captura jmeter-peticion](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/jmeter-peticion.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/jmeter-peticion.png)
#### Para visualizar los resultados añadimos
añadir -receptor- gráfico de resultados
######################################################
[![Captura jmeter-gr-res](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/jmeter-gr-res.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/jmeter-gr-res.png)
######################################################
añadir -receptor- ver árbol de resultados 
######################################################
[![Captura jmeter-arb-res](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/jmeter-arb-res.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/jmeter-arb-res.png)
#################################################
### Para las pruebas realizadas con una sola máquina obtenemos la siguiente grafica.
[![Captura jmeter-1-maq](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/jmeter-1-maq.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/jmeter-1-maq.png)
#################################################
### Para la realizar la petición http en el campo nombre de servidor o IP en mi caso la ip 192.168.56.101 de la máquina uno, en la ruta el fichero al cual queremos acceder /fichero.html
[![Captura jmeter-peticion-http](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/jmeter-peticion-http.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/jmeter-peticion-http.png)

###################################################
### Vemos el árbol de resultados.
[![Captura jmeter-resultados](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/jmeter-resultados.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/jmeter-resultados.png)
####################################################
### Comprobamos el rendimiento del balanceador con nginx
[![Captura jmeter-balanceador-nginx](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/jmeter-balanceador-nginx.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/jmeter-balanceador-nginx.png)
####################################################
### Comprobamos el rendimiento del balanceador con haproxy
[![Captura jmeter-balanceador-haproxy](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/jmeter-balanceador-haproxy.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/jmeter-balanceador-haproxy.png)

##############################################









