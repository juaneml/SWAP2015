#Práctica 5 Replicación de bases de datos MySQL.
###################################################

## Crear una BD e insertar datos
###################################################
### Nos vamos a nuestra máquina 1 ejecutamos el comando siguiente:
mysql -uroot -p
### En la opción Enter password, introducimos nuestra password o lo dejamos en blanco
####################################################
### Obtendremos el siguiente resultado.
[![Captura ini-mysql](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-5/imagenes/ini-mysql.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/ini-mysql.png)
####################################################
### Creamos una base de datos ejecutamos el comando siguiente:
create database contactos;
### Muy importante no olvidar el ";" al final de cada sentencia.
### Una vez creada nuestra base de datos ejecutamos el comando:
use contactos;
### Mostramos las tablas, como no tenemos ninguna nos mostrará que nuestra base de datos esta vacia.
show tables;
### Creamos nuestra tabla datos, ejecutamos el comando siguiente:
create table datos (nombre varchar(100),tlf int);
##### Donde datos es el nombre de la tabla, entre paréntesis son los tipos de datos, nombre de tipo varchar y tlf de tipo entero.

### Mostramos nuestra tabla creada con el comando siguiente:
show tables;
#####################################################
### Obtendremos el siguiente resultado:
[![Captura mysql-1](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-5/imagenes/mysql-1.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/mysql-1.png)
### Para mostrar el contenido de nuestra tabla utiliamos el comando siguiente:
select * from datos;

### Para ver el tipo de datos que tiene nuestra tabla utilizamos el comando siguiente:
describe datos;

### Obtendremos el siguiente resultado:
[![Captura mysql-2](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-5/imagenes/mysql-2.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/mysql-2.png)

## Replicar una BD MySQL con mysqldump
#####################################################

### En el servidor de BD principal ejecutamos los comandos siguientes:
mysql -u root -p
##########################
mysql > FLUSH TALBES WITH READ LOCK;
############################
mysql > quit

######################################################
### Obtendremos el siguiente resultado:
[![Captura mysql-dump](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-5/imagenes/mysql-dump.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/mysql-dump.png)
### En el servidor principal ejecutamos el comando siguiente:
mysqldump contactos -u root -p > /root/contactos.sql

### Como habíamos bloqueado las tablas, debemos desbloquearlas para ello utiliamos el comando siguiente:
mysql -u root -p
###########################################
mysql> UNLOCK TABLES;
###########################################
mysq> quit

### Obtendremos el siguiente resultado:
[![Captura mysql-dump-2](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-5/imagenes/mysql-dump-2.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/mysql-dump-2.png)

### Una vez que lo hemos hecho nos vamos a nuestra segunda máquina para copiar el archivo .sql, ejecutamos el comando siguiente:

scp root@192.168.56.101:/root/contactos.sql /root/
### Obtendremos el siguiente resultado:
[![Captura copia-maq2-scp](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-5/imagenes/copia-maq2-scp.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/copia-maq2-scp.png)
### Con el archivo de copia de seguridad en el esclavo ya podemos importar la BD completa en el MySQL.
#### Creamos la BD:
mysql -u root -p
##################################
mysql> CREATE DATABASE 'contactos';
##################################
mysql> quit

#### Restauramos los datos contenidos en la BD:
mysql -u root -p contactos \< /root/contactos.sql
#########################################################

##Replicación de BD mediante una configuración maestro-esclavo
############################################################
### Nos vamos a nuestra máquina maestro.
### Con el editor nano como root modificamos /etc/mysql/my.cnf
nano /etc/mysql/my.cnf
#### Comentamos el parámetro bind-address.
\# bind-address 127.0.0.1
#### Le indicamos el archivo donde almacenar el log de errores.
log_error = /var/log/mysql/error.log
#### Establecemos el identificador del servidor.
server-id = 1
#### Descomentamos el registro binario.
log_bin = /var/log/mysql/bin.log
################################################################
[![Captura config-maestro](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-5/imagenes/config-maestro.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/config-maestro.png)

#### Guardamos el documento y reiniciamos el servicio:
/etc/init.d/mysql restart

### Finalizada la configuración maestro, nos vamos a nuestra máquina esclavo.
### Con el editor nano como root modificamos /etc/mysql/my.cnf
nano /etc/mysql/my.cnf
#### Comentamos el parámetro bind-address.
\#bind-address 127.0.0.1
#### Le indicamos el archivo donde almacenar el log de errores.
log_error = /var/log/mysql/error.log
#### Establecemos el identificador del servidor.
server-id = 2
#### Descomentamos el registro binario.
log_bin = /var/log/mysql/bin.log
[![Captura config-esclavo](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-5/imagenes/config-esclavo.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/config-esclavo.png)
#### Guardamos el documento y reiniciamos el servicio:
/etc/init.d/mysql restart

### Volvemos a la máquina maestro.
### Iniciamos mySQL.
mysql -u root -p
### Ejecutamos los siguientes comandos:
mysql> CREATE USER esclavo IDENTIFIED BY 'esclavo';
######################################################
mysql> GRANT REPLICATION SLAVE ON *.* TO 'esclavo'@'%'
######################################################
IDENTIFIED BY 'esclavo';
######################################################
mysql> FLUSH PRIVILEGES;
######################################################
mysql> FLUSH TABLES;
######################################################
mysql> FLUSH TABLES WITH READ LOCK;

### Para finalizar ejecutamos un último comando:
mysql> SHOW MASTER STATUS;
#####################################
### Obtendremos el siguiente resultado:
[![Captura crea-esclavo](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-5/imagenes/crea-esclavo.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/crea-esclavo.png)
##########################################
### Donde tenemos que tener especial cuidado en el campo File y Position ya que estos resultados tenemos que ponerlos en nuestra máquina esclavo.

### Nos vamos a nuestra máquina esclavo.
### Iniciamos MySQL:
mysql -u root -p

### Ejecutamos los comandos siguientes:
mysql> CHANGE MASTER TO MASTER_HOST='192.168.56.101',
########################################################
MASTER_USER='esclavo', MASTER_PASSWORD='esclavo',
########################################################
MASTER_LOG_FILE='mysql-bin.000003', MASTER_LOG_POS=869,
########################################################
MASTER_PORT=3306;

### Por último ejecutamos:
mysql> START SLAVE;
##########################################################
[![Captura start-slave](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-5/imagenes/start-slave.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/start-slave.png)
###############################################################

### Volvemos a la máquina maestro ejecutamos el comando siguiente:
mysql> UNLOCK TABLES;

### En la máquina esclavo ejecutamos el comando siguiente:
mysql> SHOW SLAVE STATUS\G
####################################################
### Obtendremos el siguiente resultado:
[![Captura show-slave-status](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-5/imagenes/show-slave-status.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/show-slave-status.png)
#######################################################
### Para comprobar que todo ha ido bien y funciona nos vamos a la máquina maestro e insertamos una tupla:

mysql> use contactos;
############################################################
mysql> insert into datos(nombre,tlf) values("paco",958745636);
#########################################################
mysql quit
############################################################
[![Captura prueba-insert-maq1](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-5/imagenes/prueba-insert-maq1.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/prueba-insert-maq1.png)

### Vamos a la máquina esclavo y comprobamos que los datos han sido replicados:
mysql> select * from datos;

### Como podemos ver en la siguiente captura, los datos han sido replicados.
[![Captura prueba-insert-result](https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-5/imagenes/prueba-insert-result.png)]
(https://github.com/juaneml/SWAP2015/blob/master/PRACTICAS/Practica-4/imagenes/prueba-insert-result.png)
#############################################################

