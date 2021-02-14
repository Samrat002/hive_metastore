
# hive_metastore
A docker based hive-metastore service that can be used for deploying metastore service as seperate and break the coupling from the hadoop architecture.


## STEPS FOR SETUP 

1) clone this repo 
    ```
    git clone <this repo>
    ```
    
    
2) Hive Standalone metastore download
   ```
      
      wget https://repo1.maven.org/maven2/org/apache/hive/hive-standalone-metastore/3.1.2/hive-standalone-metastore-3.1.2-bin.tar.gz
      tar -xvf hive-standalone-metastore-3.1.2-bin.tar.gz
      rm -f hive-standalone-metastore-3.1.2-bin.tar.gz  
      mv apache-hive-metastore-3.1.2-bin metastore
   ```
   
3) Download hadoop 3.2.1
    ```
    wget http://apache.mirrors.hoobly.com/hadoop/common/hadoop-3.2.1/hadoop-3.2.1.tar.gz
    tar -xvf hadoop-3.2.1.tar.gz
    rm -f hadoop-3.2.1.tar.gz
    ```
    
4) We are using postgres as a database for the metastore service. Download the postgres jdbc jar 
  ```
  wget https://jdbc.postgresql.org/download/postgresql-42.2.16.jar
  ```

5) Create docker image 
  ```
  docker build -t hive_metastore_service_image:1.0 .
  ```
 
6) Run Hive metastore service 
  ```
  docker run -d -p 9083:9083/tcp --name hive_metatstore hive_metastore_service_image
  ```

