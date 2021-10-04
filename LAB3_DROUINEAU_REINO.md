# Apache Hive

## 1.1 Create a connection to Beeline Client
+ Which command allows you to view the jdbc connection used to connectto HiveServer2 ?
 #### It's the command : 
    !list
![image](https://user-images.githubusercontent.com/55360061/135850337-3ac17618-2b5b-472b-a676-8ff81eced9ec.png)

+ List all databases
#### It's the command :
    SHOW DATABASES;
    
    +-----------------------+
    |  database_name	  |
    +-----------------------+
    | armel           	|
    | balthazar_r     	|
    | baudouindlv     	|
    | bcimetiere      	|
    | bclaudic        	|
    | berenice        	|
    | cedric_kabore   	|
    | cgrandclaude    	|
    | cjdidi          	|
    | cmauvezin       	|
    | default         	|
    | e_diez          	|
    | e_guedj         	|
    | eya_database    	|
    | eya_gheyouche   	|
    | gudronlauret    	|
    | gugulpb         	|
    | hive1           	|
    | i_aderdour      	|
    | ilyass_bourkaik 	|
    | information_schema    |
    | jbenayad        	|
    | jcrecel         	|
    | l_etzol         	|
    | l_ferrand       	|
    | l_maiz          	|
    | llecomte        	|
    | lucas_maiz      	|
    | m_abatti        	|
    | ma_baseismail   	|
    | mame            	|
    | mame_aicha_dieye	|
    | marieblein      	|
    | mbourabah       	|
    | mdufau          	|
    | mhanania        	|
    | mhatoum         	|
    | ncailleux       	|
    | ninon           	|
    | ntharmaseelan   	|
    | pmeignan        	|
    | rbocchini       	|
    | rbouderghouma   	|
    | revillon        	|
    | sghlouci        	|
    | spiquet         	|
    | svassent        	|
    | sys             	|
    | temp            	|
    | vaihau_williamu 	|
    | vincent_ly      	|
    | wang_ye         	|
    | wangye          	|
    | yang_chen       	|
    | ymaassouli      	|
    +-----------------------+
    55 rows selected (0,214 seconds)

+ If not exists, create a database using your username
#### It's the command : 
    CREATE DATABASE adrouineau_areino;
    
+ Use your database
#### It's the command : 
    USE adrouineau_areino;
     
+ List the tables
#### It's the command :
    SHOW TABLES;
    +-----------+
    | tab_name  |
    +-----------+
    +-----------+

+ Create table called temp with a column col of String type
#### It's the command : 
    CREATE TABLE temp (col String);
    
+ Confirm the table creation
#### It's the command :
    SHOW TABLES;
    +-----------+
    | tab_name  |
    +-----------+
    |  temp     |
    +-----------+
+ List the columns of temp table
#### It's the command : 
    SHOW COLUMNS IN temp;
    +--------+
    | field  |
    +--------+
    | col	 |
    +--------+

+ Remove the table
#### It's the command :
    DROP TABLE temp;
    +-----------+
    | tab_name  |
    +-----------+
    +-----------+
# 1.2 Create tables
+ Create an external table called treesexternal
#### The command is : 
    CREATE EXTERNAL TABLE IF NOT EXISTS trees_external(Geopoint STRING,Arrondissement INT,Genre STRING,Espece STRING,Famille STRING,AnneePlantation INT,Hauteur FLOAT,Circonference FLOAT,Adresse STRING,NomCommun STRING,Variete STRING,ObjectId INT,NomEv STRING) 
    COMMENT "Trees of Paris" 
    ROW FORMAT DELIMITED 
    FIELDS TERMINATED BY "\u003B" 
    STORED AS TEXTFILE 
    LOCATION "/user/a.drouineau/treesParis";

+ Create an internal table called treesinternal
#### The command is :
    CREATE TABLE IF NOT EXISTS trees_internal(Geopoint STRING,Arrondissement INT,Genre STRING,Espece STRING,Famille STRING,AnneePlantation INT,Hauteur FLOAT,Circonference FLOAT,Adresse STRING,NomCommun STRING,Variete STRING,ObjectId INT,NomEv STRING) 
    COMMENT "Trees of Paris" 
    ROW FORMAT DELIMITED 
    FIELDS TERMINATED BY "\u003B";

+ Import data to the internal table using the external table
#### Here we had to use the command : set hive.execution.engine=mr because we had issues with Tez
#### The command to import data in the internal table from external table is :
    insert overwrite table trees_internal select * from trees_external;

+ Verify that each table got the same lines count
#### commands to verify are : 
    select count(*) from trees_external
    +------+
    | _c0  |
    +------+
    | 98   |
    +------+
#### and for internal table :
    select count(*) from trees_internal
    +------+
    | _c0  |
    +------+
    | 98   |
    +------+

