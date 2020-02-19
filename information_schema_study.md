# Information Schema 

Análisis sobre contenido, información importante y comentarios

    use information_schema;
    show tables; 

    describe INNODB_SYS_TABLESTATS;
    select * from INNODB_BUFFER_POOL_STATS;
    select * from INNODB_LOCKS;
    select * from INNODB_LOCK_WAITS;
    select * from INNODB_SYS_INDEXES;
    select * from INNODB_SYS_TABLESPACES; -- FILE_FORMAT averiguar el significado de Barracuda y Antelope
    select * from INNODB_METRICS; -- tiene una columna, SUBSYSTEM parametro lock, la cual sirve para ver cuantas veces se ha bloqueado algo por alguna query

    select * from VIEWS; -- hay hartas vistas del schema sys para analizar, que presentan estadisticas e informacion para ayudar en la optimizacion
    select * from USER_PRIVILEGES;
    select * from TRIGGERS; -- sirve para validar la forma en que se define el usuario, validar cuando esta con %
    select * from TABLE_PRIVILEGES;
    select * from STATISTICS;
    select * from SESSION_VARIABLES; -- error, disabled revisar en version 5.7
    select * from SESSION_STATUS; -- mismo anterior
    select * from SCHEMA_PRIVILEGES;
    select * from SCHEMATA; -- informacion sobre los distintos schemas de la bd, sirve para ver DEFAULT_CHARACTER_SET_NAME, averiguar sobre SQL_PATH
    select * from PROCESSLIST; -- lista los procesos, es como verlos en mysql workbench
    select * from PROFILING; -- tiene un monton de columnas, al parecer no tiene datos por el poco uso de la bd
    select * from OPTIMIZER_TRACE;
    select * from KEY_COLUMN_USAGE;
    select * from EVENTS;
    
Por el momento son las tablas que encontré interesantes de analizar y conocer su contenido, ya que entregan información del motor INNODB y sobre las consultas y tablas de los distintos schemas.
