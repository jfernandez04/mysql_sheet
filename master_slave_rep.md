 # Mysql Master-Slave Replication
 
  La arquitectura maestro servidor puede ser utilizada para separar tareas de un sistema web, donde el servidor maestro es el encargado de leer y escribir datos (consulta de datos propias del sistema) mientras que el servidor esclavo se utiliza para consultar información de reportes.
  
  agregar imágen arquitectura
   ##Servidor Master
   
   Todas las configuraciones se hacen en /etc/mysql/my.cnf o donde esté ubicado el archivo de configuración de mysql.
    server-id               = 1 

   Es el identificador del servidor Master

    bind-address            = 127.0.0.1
   Es la ip con la cual identificar el servidor
    
    log_bin                 = /var/log/mysql/mysql-bin.log
   Este es la ubicación donde se guardaran los datos desde donde el esclavo leerá
   
    binlog_do_db            = newdatabase
   Indica que base de datos se leerá
   
    sudo service mysql restart
   Reinicia el servidor
   
    mysql -u root -p
    GRANT REPLICATION SLAVE ON *.* TO 'slave_user'@'%' IDENTIFIED BY 'password';
    FLUSH PRIVILEGES;
    SHOW MASTER STATUS;
    
    mysql> SHOW MASTER STATUS;
    +------------------+----------+--------------+------------------+
    | File             | Position | Binlog_Do_DB | Binlog_Ignore_DB |
    +------------------+----------+--------------+------------------+
    | mysql-bin.000001 |      107 | newdatabase  |                  |
    +------------------+----------+--------------+------------------+
    1 row in set (0.00 sec)
    
   Nos conectamos al servidor, asignamos permisos de replicación al usuario slave y password 'password'.
   El comando show MASTER stagus\G nos muestra el estado una vez iniciado el servidor como maestro.
   
    mysqldump -u root -p --opt newdatabase > newdatabase.sql
   Hacemos un dump (volcado) de la base de datos para cargar en el esclavo.
    
    
##Servidor Slave

    CREATE DATABASE newdatabase;
    mysql -u root -p newdatabase < /path/to/newdatabase.sql
    server-id               = 2
    relay-log               = /var/log/mysql/mysql-relay-bin.log
    log_bin                 = /var/log/mysql/mysql-bin.log
    binlog_do_db            = newdatabase
    CHANGE MASTER TO MASTER_HOST='12.34.56.789',MASTER_USER='slave_user', MASTER_PASSWORD='password', 
    MASTER_LOG_FILE='mysql-bin.000001', MASTER_LOG_POS=  107;
    START SLAVE;
    SHOW SLAVE STATUS\G
    
    
https://dev.mysql.com/doc/refman/5.7/en/change-master-to.html