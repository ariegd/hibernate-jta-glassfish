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

## Creando JDBC Connection Pool
-------------------------------
![jdbc-connection-pool(Derby)](https://github.com/ariegd/hibernate-jta-glassfish/assets/24771696/0bfe85ee-581b-4d02-a2ef-469904738885)
![jdbc-connection-pool(Derby)2](https://github.com/ariegd/hibernate-jta-glassfish/assets/24771696/157b6b2b-99d9-4198-abf2-f7e5ad6e92b4)
![jdbc-connection-pool(H2)](https://github.com/ariegd/hibernate-jta-glassfish/assets/24771696/2026166f-1fc9-44ca-806d-53814334aa0d)
![jdbc-connection-pool(H2)2](https://github.com/ariegd/hibernate-jta-glassfish/assets/24771696/22d97868-ab87-4423-812c-f3031e99153e)
![jdbc-connection-pool(HSQLDB)](https://github.com/ariegd/hibernate-jta-glassfish/assets/24771696/7a768d66-f427-42b7-9514-a0d3b139354c)
![jdbc-connection-pool(HSQLDB)2](https://github.com/ariegd/hibernate-jta-glassfish/assets/24771696/3823edca-1663-4c32-8753-07e08d86ffcc)
![jdbc-connection-pool(MySQL)](https://github.com/ariegd/hibernate-jta-glassfish/assets/24771696/693403be-d1a1-4173-943a-0a3b05b63b63)
![jdbc-connection-pool(MySQL)2](https://github.com/ariegd/hibernate-jta-glassfish/assets/24771696/7dc8a23d-2c82-4091-a3d6-13c41fdeb418)
![jdbc-connection-pool(OracleFree)](https://github.com/ariegd/hibernate-jta-glassfish/assets/24771696/9f3ce312-6d6e-416e-8265-0d55ef37afaf)
![jdbc-connection-pool(OracleFree)2](https://github.com/ariegd/hibernate-jta-glassfish/assets/24771696/6ebaf035-b0d7-431c-8244-a3964e772cdc)


