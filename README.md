# Conexión mediante JTA en Hibernate, GlassFish a bases de datos
---------------------------------------------------------------
Para comenzar a utilizar JTA, se explican los pasos a continuación. Pero lo principal es tener un servidor de aplicaciones con el recurso de acceso a la base de datos creado.

Nota: Este ejemplo obtenido del repositorio de Eclipse GlassFish

## Pasos para crear la conexión JTA en GlassFish
-----------------------------------------------

1. Primero crear la base de datos en el servidor db
Derby
H2
HSQLDB
MySQL
Oracle
PostgreSQL

2. Generalmente ir al directorio raíz servidor_db/lib compiar el *.jar en ~/glassfish-5.1.0/glassfish5/glassfish/domains/domain1/lib/ext
<Nota Para esto se puede ir a la dependencia en el POM, luego googlear en le repositorio de maven y descargar el *.jar>
derbyclient.jar
h2-2.1.214.jar
hsqldb-2.5.1.jar (from Maven repository)

3. Restart GlassFish server
./asadmin stop-domain
./asadmin start-domain

4. Crear en GlassFish ./asadmin create-jdbc-connection-pool 'JDBC Connection Pools'
::::::::::::::::::::::::::::::::::::::::::::::::::::::::: H2
./asadmin create-jdbc-connection-pool --datasourceclassname  org.h2.jdbcx.JdbcDataSource --restype javax.sql.DataSource --property user=zodd:password=zodd:url="jdbc\\:h2\\:tcp\\://localhost\\.\\:h2database\\:gfdb" h2-pool
::::::::::::::::::::::::::::::::::::::::::::::::::::::::: MySQL
./asadmin create-jdbc-connection-pool --datasourceclassname  com.mysql.cj.jdbc.MysqlDataSource --restype javax.sql.DataSource --property user=zodd:password=zodd:url="jdbc\\:mysql\\://localhost\\:3306/gfdb" _mysql

jdbc:mysql://localhost:3306/db?allowPublicKeyRetrieval=true&useSSL=false

> Nota: Si en el --restype en ves de 'javax.sql.DataSource', colocas 'java.sql.Driver' debes colocar el Driver Classname.

5. Luego hacer las modificaciones pertinentes y crear el 'JDBC Resources' graficamente

