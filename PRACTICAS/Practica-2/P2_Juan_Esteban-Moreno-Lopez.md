#Práctica 2

## Funcionamiento de la copia de archivos por ssh.

#######################################################
 
#### Queremos copiar un directorio de nuestra máquina uno a una segunda máquina.
Creamos un tar con ficheros locales en un equipo remoto.

##########################################################

Para ello utizamos el comando tar y ssh de la siguiente forma:

##### tar czf - ./ | ssh roo@192.168.56.102 'cat > ~/tar.tgz'
Donde ./ es el directorio, root@192.168.56.102 es nuestra seguda máquina.

##############################################################################

#### En la siguiente captura podemos observar que la ejecución del comando se ha realizado con éxito.
[![Captura shh](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-2/imagenes/ssh-tar-1.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-2/imagenes/ssh-tar-1.png)

################################################################

#### En la máquina dos hacemos un listado con el comando "ls -l"  para visualizar los archivos y vemos que se ha creado con éxito nuestro archivo "tar.tgz" en la  siguiente captura de pantalla.
[![Captura shh](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-2/imagenes/ssh-tar-2.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-2/imagenes/ssh-tar-2.png)

#####################################################

## Clonado de una carpeta entre las dos máquinas.

#############################################################

Para el clonado de una carpeta entre dos máquinas, contamos con la herramienta rsync.
Lo primero que debemos de hacer es instalar la herramienta desde  el usuario root con el siguiente comando:

#### apt-get install rsync.

####################################################################

Ahora vamos a probar el funcionamiento, clonamos la carpeta con el contenido del servidor web, ejecutaremos 
el siguiente comando:

#### rsync -avz -e ssh root@192.168.56.101:/var/www/ /var/www/

#####################################################################

En la siguiente captura podemos observar que se ha realizado con éxito.

#######################################################################

[![Captura shh](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-2/imagenes/rsync-1.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-2/imagenes/rsync-1.png)

##########################################################################

Comprobamos que se ha clonado el contenido de la máquina 1 a la máquina 2 donde queremos que se clone en la siguiente
captura.

######################################################################################

[![Captura shh](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-2/imagenes/rsync-2.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-2/imagenes/rsync-2.png)

######################################################################################

Mediante ssh-keygen podemos generar la clave, con la opción -t para el tipo de clave.
Así, en la máquina secundaria ejecutaremos:

#### ssh-keygen -t dsa

#####################################################################################

Obtendremos algo parecido a esto.

#####################################################################################

[![Captura shh](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-2/imagenes/ssh-keygen-1.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-2/imagenes/ssh-keygen-1.png)

######################################################################################

## Configuración de ssh para acceder sin que solicite contraseña.
Probamos que hemos configurado correctamente nuestra máquina dos. En la siguiente captura podemos ver he hemos 
tenido éxito.

######################################################################################

[![Captura shh](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-2/imagenes/ssh-sin-password-1.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-2/imagenes/ssh-sin-password-1.png)

#########################################################################################

## Establecer una tarea en cron que se ejecute cada hora para mantener actualizado el contenido del directorio /var/www entre las dos máquinas.

#############################################################################################

Con el comando nano editamos el archivo que está alojado en /etc/crontab de la siguiente forma nano /etc/crontab

################################################################################################

 Añadimos en el archivo la siguiente línea para establecer la tarea en cron para que se ejecute cada hora.

##############################################################################################

rsync -avz --delete --exclude=**/stats --exclude=**/error --exclude=**/files/pictures-e "ssh -l root" root@192.168.56.101 :/var/www/ /var/www/

#################################################################################################

En la siguiente captura podemos ver la configuración.

##################################################################################################

[![Captura shh](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-2/imagenes/crontab.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-2/imagenes/crontab.png)




