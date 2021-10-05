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
# 1.3 Create Queries

+ displays the list of distinct containing trees
#### The query : 
    select distinct famille from trees_internal;
    
    +----------------+
    |	famille 	|
    +----------------+
    | Araucariaceae  |
    | Betulaceae 	|
    | Bignoniaceae   |
    | Cannabaceae	|
    | Cornaceae  	|
    | Cupressaceae   |
    | Ebenaceae  	|
    | Eucomiaceae	|
    | FAMILLE    	|
    | Fabaceae   	|
    | Fagaceae   	|
    | Ginkgoaceae	|
    | Juglandaceae   |
    | Magnoliaceae   |
    | Malvaceae  	|
    | Moraceae   	|
    | Oleaceae   	|
    | Paulowniaceae  |
    | Pinaceae   	|
    | Platanaceae	|
    | Sapindacaees   |
    | Sapindaceae	|
    | Simaroubaceae  |
    | Taxaceae   	|
    | Taxodiaceae	|
    | Ulmaceae   	|
    +----------------+

+ displays the list of different species trees
#### The query :
    select distinct espece from trees_internal;
    
    +-----------------+
    | 	espece  	|
    +-----------------+
    | ESPECE      	|
    | araucana    	|
    | atlantica   	|
    | australis   	|
    | baccata     	|
    | bignonioides	|
    | biloba      	|
    | bungeana    	|
    | cappadocicum	|
    | carpinifolia	|
    | colurna     	|
    | coulteri    	|
    | decurrens   	|
    | dioicus     	|
    | distichum   	|
    | excelsior   	|
    | fraxinifolia	|
    | giganteum   	|
    | giraldii    	|
    | glutinosa   	|
    | grandiflora 	|
    | hippocastanum   |
    | ilex        	|
    | involucrata 	|
    | japonicum   	|
    | kaki        	|
    | libanii     	|
    | monspessulanum  |
    | nigra       	|
    | nigra laricio   |
    | opalus      	|
    | orientalis  	|
    | papyrifera  	|
    | petraea     	|
    | pomifera    	|
    | pseudoacacia	|
    | sempervirens	|
    | serrata     	|
    | stenoptera  	|
    | suber       	|
    | sylvatica   	|
    | tomentosa   	|
    | tulipifera  	|
    | ulmoides    	|
    | virginiana  	|
    | x acerifolia	|
    +-----------------+

+ the number of trees of each kind
#### The query :
    select genre,count(genre) from trees_internal group by genre;
    
    +-----------------+------+
    |  	genre  	| _c1  |
    +-----------------+------+
    | Acer        	| 3	|
    | Aesculus    	| 3	|
    | Ailanthus   	| 1	|
    | Alnus       	| 1	|
    | Araucaria   	| 1	|
    | Broussonetia	| 1	|
    | Calocedrus  	| 1	|
    | Catalpa     	| 1	|
    | Cedrus      	| 4	|
    | Celtis      	| 1	|
    | Corylus     	| 3	|
    | Davidia     	| 1	|
    | Diospyros   	| 4	|
    | Eucommia    	| 1	|
    | Fagus       	| 8	|
    | Fraxinus    	| 1	|
    | GENRE       	| 1	|
    | Ginkgo      	| 5	|
    | Gymnocladus 	| 1	|
    | Juglans     	| 1	|
    | Liriodendron	| 2	|
    | Maclura     	| 1	|
    | Magnolia    	| 1	|
    | Paulownia   	| 1	|
    | Pinus       	| 5	|
    | Platanus    	| 19   |
    | Pterocarya  	| 3	|
    | Quercus     	| 4	|
    | Robinia     	| 1	|
    | Sequoia     	| 1	|
    | Sequoiadendron  | 5	|
    | Styphnolobium   | 1	|
    | Taxodium    	| 3	|
    | Taxus       	| 2	|
    | Tilia       	| 1	|
    | Ulmus       	| 1	|
    | Zelkova     	| 4	|
    +-----------------+------+

    
    
+ calculates the height of the tallest tree of each kind
#### The query :
    select genre,max(hauteur) from trees_internal group by genre;
    +-----------------+-------+
    |  	genre  	|  _c1  |
    +-----------------+-------+
    | Acer        	| 16.0  |
    | Aesculus    	| 30.0  |
    | Ailanthus   	| 35.0  |
    | Alnus       	| 16.0  |
    | Araucaria   	| 9.0   |
    | Broussonetia	| 12.0  |
    | Calocedrus  	| 20.0  |
    | Catalpa     	| 15.0  |
    | Cedrus      	| 30.0  |
    | Celtis      	| 16.0  |
    | Corylus     	| 20.0  |
    | Davidia     	| 12.0  |
    | Diospyros   	| 14.0  |
    | Eucommia    	| 12.0  |
    | Fagus       	| 30.0  |
    | Fraxinus    	| 30.0  |
    | GENRE       	| NULL  |
    | Ginkgo      	| 33.0  |
    | Gymnocladus 	| 10.0  |
    | Juglans     	| 28.0  |
    | Liriodendron	| 35.0  |
    | Maclura     	| 13.0  |
    | Magnolia    	| 12.0  |
    | Paulownia   	| 20.0  |
    | Pinus       	| 30.0  |
    | Platanus    	| 45.0  |
    | Pterocarya  	| 30.0  |
    | Quercus     	| 31.0  |
    | Robinia     	| 11.0  |
    | Sequoia     	| 30.0  |
    | Sequoiadendron  | 35.0  |
    | Styphnolobium   | 10.0  |
    | Taxodium    	| 35.0  |
    | Taxus       	| 13.0  |
    | Tilia       	| 20.0  |
    | Ulmus       	| 15.0  |
    | Zelkova     	| 30.0  |
    +-----------------+-------+

+ sort the trees height from smallest to largest
#### The query :
    select genre,hauteur from trees_internal order by hauteur ASC;
    +-----------------+----------+
    |  	genre  	| hauteur  |
    +-----------------+----------+
    | Sequoiadendron  | NULL 	|
    | GENRE       	| NULL 	|
    | Fagus       	| 2.0  	|
    | Taxus       	| 5.0  	|
    | Cedrus      	| 6.0  	|
    | Araucaria   	| 9.0  	|
    | Styphnolobium   | 10.0 	|
    | Quercus     	| 10.0 	|
    | Gymnocladus 	| 10.0 	|
    | Fagus       	| 10.0 	|
    | Pinus       	| 10.0 	|
    | Robinia     	| 11.0 	|
    | Diospyros   	| 12.0 	|
    | Zelkova     	| 12.0 	|
    | Diospyros   	| 12.0 	|
    | Eucommia    	| 12.0 	|
    | Acer        	| 12.0 	|
    | Magnolia    	| 12.0 	|
    | Broussonetia	| 12.0 	|
    | Davidia     	| 12.0 	|
    | Maclura     	| 13.0 	|
    | Taxus       	| 13.0 	|
    | Pinus       	| 14.0 	|
    | Diospyros   	| 14.0 	|
    | Diospyros   	| 14.0 	|
    | Acer        	| 15.0 	|
    | Catalpa     	| 15.0 	|
    | Fagus       	| 15.0 	|
    | Ulmus       	| 15.0 	|
    | Quercus     	| 15.0 	|
    | Zelkova     	| 16.0 	|
    | Acer        	| 16.0 	|
    | Celtis      	| 16.0 	|
    | Alnus       	| 16.0 	|
    | Aesculus    	| 18.0 	|
    | Ginkgo      	| 18.0 	|
    | Zelkova     	| 18.0 	|
    | Fagus       	| 18.0 	|
    | Calocedrus  	| 20.0 	|
    | Sequoiadendron  | 20.0 	|
    | Fagus       	| 20.0 	|
    | Platanus    	| 20.0 	|
    | Platanus    	| 20.0 	|
    | Corylus     	| 20.0 	|
    | Taxodium    	| 20.0 	|
    | Corylus     	| 20.0 	|
    | Corylus     	| 20.0 	|
    | Paulownia   	| 20.0 	|
    | Tilia       	| 20.0 	|
    | Platanus    	| 20.0 	|
    | Liriodendron	| 22.0 	|
    | Pterocarya  	| 22.0 	|
    | Aesculus    	| 22.0 	|
    | Ginkgo      	| 22.0 	|
    | Platanus    	| 22.0 	|
    | Fagus       	| 23.0 	|
    | Platanus    	| 25.0 	|
    | Ginkgo      	| 25.0 	|
    | Pinus       	| 25.0 	|
    | Ginkgo      	| 25.0 	|
    | Cedrus      	| 25.0 	|
    | Platanus    	| 25.0 	|
    | Platanus    	| 26.0 	|
    | Platanus    	| 27.0 	|
    | Pterocarya  	| 27.0 	|
    | Juglans     	| 28.0 	|
    | Sequoiadendron  | 30.0 	|
    | Pterocarya  	| 30.0 	|
    | Cedrus      	| 30.0 	|
    | Fagus       	| 30.0 	|
    | Platanus    	| 30.0 	|
    | Cedrus      	| 30.0 	|
    | Platanus    	| 30.0 	|
    | Taxodium    	| 30.0 	|
    | Pinus       	| 30.0 	|
    | Quercus     	| 30.0 	|
    | Sequoia     	| 30.0 	|
    | Fagus       	| 30.0 	|
    | Aesculus    	| 30.0 	|
    | Zelkova     	| 30.0 	|
    | Pinus       	| 30.0 	|
    | Fraxinus    	| 30.0 	|
    | Sequoiadendron  | 30.0 	|
    | Quercus     	| 31.0 	|
    | Platanus    	| 31.0 	|
    | Platanus    	| 32.0 	|
    | Ginkgo      	| 33.0 	|
    | Platanus    	| 34.0 	|
    | Taxodium    	| 35.0 	|
    | Platanus    	| 35.0 	|
    | Ailanthus   	| 35.0 	|
    | Sequoiadendron  | 35.0 	|
    | Liriodendron	| 35.0 	|
    | Platanus    	| 40.0 	|
    | Platanus    	| 40.0 	|
    | Platanus    	| 40.0 	|
    | Platanus    	| 42.0 	|
    | Platanus    	| 45.0 	|
    +-----------------+----------+

+ displays the district where the oldest tree is
#### The query :
    select arrondissement from trees_internal where hauteur = (select max(hauteur) from trees_internal);
    
    +-----------------+
    | arrondissement  |
    +-----------------+
    | 12          	|
    +-----------------+

+ displays the district that contains the most trees
#### The query :
    SELECT arrondissement, COUNT(genre) FROM trees_internal GROUP BY arrondissement ORDER BY COUNT(genre) DESC LIMIT 1;
    +-----------------+------+
    | arrondissement  | _c1  |
    +-----------------+------+
    | 16          	| 36   |
    +-----------------+------+

