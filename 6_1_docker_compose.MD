Docker Compose 
----------------

Command line utilty to define and run multi container applications with Docker. With compose, we define the services that need tor un in a YAML file. Then bring up the services by using docker-compose command.

    wordpress:
      image: wordpress
      links:
        - mysql
      ports:
        - "80:80"
      environment:
        - WORDPRESS_DB_NAME=wordpress
        - WORDPRESS_DB_USER=wordpress
        - WORDPRESS_DB_PASSWORD=wordpresspwd 
    mysql:
      image: mysql
      environment:
        - MYSQL_ROOT_PASSWORD=wordpressdocker
        - MYSQL_DATABASE=wordpress
        - MYSQL_USER=wordpress
        - MYSQL_PASSWORD=wordpresspwd
   
   
command
--------

    docker-compose up -d
       
    docker-compose ps
    Name             Command             State              Ports       
    -------------------------------------------------------------------------
    dockercompose_my   /entrypoint.sh     Up                 3306/tcp         
    sql_1              mysqld                                                 
    dockercompose_wo   /entrypoint.sh     Up                 0.0.0.0:80->80/t 
    rdpress_1          apache2-for ...                       cp              
