#Práctica 2

## Funcionamiento de la copia de archivos por ssh.
#######################################################
 
#### Queremos copiar un directorio de nuestra máquina uno a una segunda máquina.
Creamos un tar con ficheros locales en un equipo remoto.
##########################################################
Para ello utizamos el comando tar y ssh de la siguiente forma:

##### tar czf - ./ | ssh roo@192.168.56.102 'cat > ~/tar.tgz'
Donde ./ es el directorio, root@192.168.56.102 es nuestra seguda máquina.

#### En la siguiente captura podemos observar que la ejecución del comando se
[![Captura shh](https://github.com/juaneml/SWAP2015/tree/master/PRACTICAS/Practica-2/imagenes/ssh-tar-1.png)](https://github.com/juaneml/SWAP2015/tree/master/PRACTICAS/Practica-2/imagenes/ssh-tar-1.png)
#### ha realizado con éxito.
## Clonado de una carpeta entre las dos máquinas.

## Configuración de ssh para acceder sin que solicite contraseña.

## Establecer una tarea en cron que se ejecute cada hora para mantener actualizado el contenido del directorio /var/www entre las dos máquinas.

### Con el comando nano editamos el archivo que está alojado en /etc/crontab de la siguiente forma nano /etc/crontab

### Añadimos en el archivo la siguiente línea para establecer la tarea en cron para que se ejecute cada hora.

#### rsync -avz --delete --exclude=**/stats --exclude=**/error --exclude=**/files/pictures-e "ssh -l root" root@192.168.56.101 :/var/www/ /var/www/
