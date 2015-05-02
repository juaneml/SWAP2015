#####
##Instalamos apache berksmark 
sudo apt-get install apache2-utils

[![Captura Install_ab](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/Install_ab.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-3/imagenes/edi.fic-sources.png)
##Comprobamos el funcionamiento del apache berksmark
####Para ello creamos un fichero en mi caso utilizo un fichero.php
ab -n 1000 -c 10 http://192.168.56.101/fichero.php


