
# hive_metastore
A docker based hive-metastore service that can be used for deploying metastore service as seperate and break the coupling from the hadoop architecture.


## STEPS FOR SETUP 

1) clone repository and go inside the repository
    ```
    git clone git@github.com:Samrat002/hive_metastore.git
    cd hive_metastore
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

5) update the `metastore-site.xml` file with the connection details 
    ```
    vi conf/metastore-site.xml
    ```
    
    a) replace the required user name in the `xml` with the correct username in the database
    ```
    <property>
        <name>javax.jdo.option.ConnectionUserName</name>
        <value>your user</value>
    </property>
    ```
    b) replace the password 
    ```
    <property>
        <name>javax.jdo.option.ConnectionPassword</name>
        <value>your password </value>
    </property>
    ```
    c) update the connectionURL
    ```
    <property>
        <name>javax.jdo.option.ConnectionURL</name>
        <value>jdbc:postgresql://hostname:port_number/database_name</value>
        <description>this is the connection url resposible for the connect</description>
    </property>
    ```
    

6) Create docker image 
  ```
  docker build -t hive_metastore_service_image:1.0 .
  ```
 
7) Run Hive metastore service 
  ```
  docker run -d -p 9083:9083/tcp --name hive_metatstore hive_metastore_service_image
  ```

