
# Side Notes
  If you whant to get an advice about indexes on your schema, here's two ways:

   1. Using mysqlindexcheck utility wich came from mysql-client install on most os (I'm using OsX)
      Usage ex.: mysqlindexcheck --server=root:rootsafe@10.0.2.3 db_export_prize

    2. *(Need to find other way)



 # Mysql Query Cache


SHOW VARIABLES LIKE '%query_cache%';

SHOW STATUS LIKE '%qcache%';

select @@query_cache_size/1024/1024;



SHOW ENGINE INNODB MUTEX;

SHOW ENGINE INNODB STATUS;

# Performance Schema

use performance_schema;

select * from performance_schema;

show variables like 'performance_schema';

SELECT 
    object_schema, object_name, index_name,count_read,count_write,count_fetch
FROM
    performance_schema.table_io_waits_summary_by_index_usage
WHERE
    index_name IS NOT NULL
        AND count_star < 2
        ORDER BY object_schema , OBJECT_NAME;


describe table_io_waits_summary_by_index_usage;

show global status like 'Created%'; 

select @@tmp_table_size/1024/1024/1024;


(select (@@innodb_buffer_pool_chunk_size/1024/1024/1024)/(@@innodb_buffer_pool_size/1024/1024/1024)); 

select @@innodb_buffer_pool_size/1024/1024/1024;
select @@innodb_buffer_pool_chunk_size/1024/1024/1024;

SELECT CEILING(Total_InnoDB_Bytes*1.6/POWER(1024,3)) RIBPS FROM
(SELECT SUM(data_length+index_length) Total_InnoDB_Bytes
FROM information_schema.tables WHERE engine='InnoDB' and table_schema='db_export_prize') A;


select * from information_schema.tables WHERE engine='InnoDB' and table_schema='db_export_prize';

SELECT SUM(data_length+index_length) Total_InnoDB_Bytes
FROM information_schema.tables WHERE engine='InnoDB' and table_schema='db_export_prize';

show master status;

SHOW GLOBAL STATUS LIKE 'Innodb_buffer_pool_pages_%';