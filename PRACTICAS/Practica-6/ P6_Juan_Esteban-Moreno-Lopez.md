# Configuración del RAID por sofware
## En nuestro programa de virtualización nos vamos a configuración-almacenamiento-agregar disco duro y agregamos los discos a los que vamos hacer nuestra configuración RAID.

############################################################################

## Nos quedará el siguiente resultado:

[![Captura configuración](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/configuracion.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/configuracion.png)

#############################################################################

##En la máquina que queremos hacer la configuración por RAID ejecutamos el comando siguiente:
sudo apt-get install mdadm


## Obtendremos el siguiente resultado:

[![Captura install-mdadm](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/install-mdadm.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/install-mdadm.png)

###############################################################

## Se nos iniciará la siguiente pantalla de configuración:

[![Captura mdadm-1](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/mdadm-1.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/mdadm-1.png)

## Cuando finalice la instalación obtendremos:

[![Captura mdadm-2](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/mdadm-2.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/mdadm-2.png)

## Ahora buscamos la información, identificación asignada por Linux. Ejecutamos el siguiente comando:

sudo fdisk -l

#############################################################

## Obtendremos el siguiente resultado:
[![Captura fdisk-l](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/fdisk-l.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/fdisk-l.png)

## Nos disponemos a crear el RAID 1, usando el dispositivo /dev/dm0. Ejecutamos el siguiente comando:

sudo mdadm -C /dev/md0 --level = raid1 --raid-devices=2 /dev/sdb /dev/sdc

#################################################################
[![Captura dev-md0](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/dev-md0.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/dev-md0.png)
## Si no hemos obtenido ningún error ya podemos crear el directorio en el que se montará la unidad del RAID. Ejecutamos los siguientes comandos:

sudo mkdir /datos
sudo mount /dev/md0 /datos

## Obtendremos el siguiente resultado:
[![Captura mount](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/mount.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/mount.png)

## Para comprobar el estado del RAID, ejecutamos el siguiente comando:

sudo mdadm --detail /dev/md0

##################################################################
[![Captura detail](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/detail.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/detail.png)

#########################################################################

## Para finalizar el proceso, conviene configurar el sistema para que monte el dispositvo RAID creado al arrancar el sistema. Para ello editamos el archivo /etc/fstab y añadimos la siguiente línea:

/dev/md0 /datos nodev,noexec,nosuid 0 3

###################################################################

## Obtendremos el siguiente resultado:

[![Captura fstab](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/fstab.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/fstab.png)

#############################################################

## Con el siguiente comando actualizamos y montamos el dispositivo RAID :

mount -a

#############################################################

[![Captura montado-auto](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/montado-auto.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/montado-auto.png)

## Al iniciar la máquina vemos como nos monta el RAID:

[![Captura inicio-montaje](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/inicio-montaje.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/inicio-montaje.png)

##########################################################################

## Por último vamos a configurar mdadm para simular la caida de uno de los discos. Para ello lo primero que tenemos que hacer es ejecutar el siguiente comando:

mdadm --detail --scan >> /etc/mdadm/mdadm.conf

#############################################################################
[![Captura mdadm.conf-1](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/mdadm.conf-1.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/mdadm.conf-1.png) 

###############################################################################

## Visualizamos que se a añadido. Ejecutamos el siguiente comando:
cat /etc/mdadm/mdadm.conf

#####################################################

[![Captura mdadm.conf-2](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/mdadm.conf-2.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/mdadm.conf-2.png)

## Ya estamos listos para simular la caida de un disco:

## Nos conectamos desde nuestro terminal ejecutamos:
ssh 192.168.156.103
## Visualizamos nuestros discos RAID, para ello ejecutamos el siguiente comando:

watch cat /proc/mdstat

##########################################################

[![Captura watch](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/watch.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/watch.png)

############################################################################

## Desde nuestra máquina ejecutamos el siguiente comando:

mdadm /dev/md127 --fail /dev/sdb 

###############################################################

[![Captura fail-sdb](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/fail-sdb.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/fail-sdb.png)

################################################################

## Visualizamos como nuestro disco ha caído:

[![Captura fallo-1](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/fallo-1.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/fallo-1.png)

################################################################

## Recuperamos el disco, ejecutamos el siguiente comando:

mdadm /dev/md127 -r /dev/sdb

## Como podemos ver en la siguiente captura se comienza con la recuperación del disco:

[![Captura prueba-insert-result](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/recupera-raid.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-6/imagenes/recupera-raid.png)
