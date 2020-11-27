# springboot_dockercompose

Dockerize a spring boot application with MySql using Dockerfile -Part 1
------------------------------------------------------------------------
Before We Begin:

    Ubuntu 18.04 system with root or user with sudo privileges
    build tool Gradle Installed
    Docker Installed 
    
    In this tutorial, we will first be creating a Spring Boot + MYSQL application and build using locally installed Gradle. We will then see how this application will be deployed on docker.
    
    step 1 –Setup MySQL docker container :
    -----------------------------------------
    docker run -d -p 3308:3306 --name=docker-mysql --env="MYSQL_ROOT_PASSWORD=root" --env="MYSQL_PASSWORD=root" --env="MYSQL_DATABASE=book_manager" mysql
    
    Login into mysql container:
    docker exec -it docker-mysql bash;
    
   This mysql 8 does not allow root login with password.so run below command to login into mysql .
   
   mysql
   
   ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root';
   FLUSH PRIVILEGES;
   CREATE DATABASE book_manager;
   exit
   
   Try again login mysql by root with password :
   mysql -u root -p
   -------------------------------------------------------------------
   Import mysql script from the project folder to mysql container:
   
    docker exec -i docker-mysql mysql -uroot -proot book_manager < ~/springbootdockercompose/sql/book_manager.sql

Build the project using Gradle from the local machine:
