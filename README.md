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
    
 
   mysql -u root -p
   -------------------------------------------------------------------
   Import mysql script from the project folder to mysql container:
   
    docker exec -i docker-mysql mysql -uroot -proot book_manager < ~/springbootdockercompose/sql/book_manager.sql

Build the project using Gradle from the local machine:

gradle build

Check whether the jar file  is generated on the projectfolder/build/libs/

Create Docker file for java 8 with snapshot jar from the machine:

FROM java:8
VOLUME /home/docker/spring_boot1 
EXPOSE 10222
COPY /build/libs/book-manager-1.0-SNAPSHOT.jar book-manager-1.0-SNAPSHOT.jar 
ENTRYPOINT ["java","-jar","book-manager-1.0-SNAPSHOT.jar"]

Build docker image from this Dockerfile
docker build -f Dockerfile -t book_manager_app .

run app container with mysql :

docker run -t --link docker-mysql:mysql -p 10222:10222 --name spring_boot book_manager_app

check th application running on 

http://localhost:10222/book


If you are using docker-compose:
--------------------------------
Clone the repo
build the project using gradele build
Depending on the folder your application jar file name will change

Run the docker compose : docker-compose up









