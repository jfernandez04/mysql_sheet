#Mysql Optimization Related stuff

  If you whant to get an advice about indexes on your schema, here's two ways:

   1. Using mysqlindexcheck utility wich came from mysql-client install on most os (I'm using OsX)
      Usage ex.: mysqlindexcheck --server=root:rootsafe@10.0.2.3 db_export_prize

    2. *(Need to find other way)



 #Mysql Query Cache


SHOW VARIABLES LIKE '%query_cache%';

SHOW STATUS LIKE '%qcache%';

select @@query_cache_size/1024/1024;
