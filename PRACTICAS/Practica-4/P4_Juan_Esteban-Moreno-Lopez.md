#Práctica 4. Comprobar el rendimiento de servidores web
#####
##Instalamos apache berksmark 
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
### Utilizamos una tercera herramienta para medir el rendimiento de servidores.
### Se trata de la herramienta Jmeter.
########################################################3
### Procedemos a su instalación con el comando.
sudo apt-get install jmeter
#######################################################
### Captura instalación.
[![Captura install-jmeter](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/install-jmeter.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/install-jmeter.png)
###########################################################
##### Fin Instalación.
[![Captura fin-install-jmeter](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/fin-install-jmeter.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/fin-install-jmeter.png)
############################################################
### Comprobamos que se ha instalado correctamente.
#################################################
### Captura.
[![Captura comp-instalacion-jmeter](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/comp-instalacion-jmeter.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/comp-instalacion-jmeter.png)
##############################################
### Iniciamos el programa con el comando:
jmeter
### Iniciamos la interfaz gráfica:
##########################################
[![Captura inicio-jmeter](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/inicio-jmeter.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/inicio-jmeter.png)
#Comprobamos el rendimiento con Jmeter

