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

### Lanzamos el programa con el siguiente comando:
 
ab -n 1000 -c 10 http://192.168.56.101/fichero.php

### Obtendremos un resultado parecido al siguiente:
[![Captura Fichero_php](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/ab-1.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/ab-1.png)
######################################################
[![Captura Fichero_php](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/ab-cap.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/ab-cap.png)


