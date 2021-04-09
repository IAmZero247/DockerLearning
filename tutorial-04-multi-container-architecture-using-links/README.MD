# Docker Tutorial 04 - Multi container architecture using docker   

1. --link
2. docker-compose

## Link
------- 

#### Use case : Start two busybox containers and create link between them 

 

	  
1.	Busy Box 1 

      `docker run --name cbb10 -it   busybox`
	  
	  ```
	  To exit from INTERACTIVE SHELLL of a container 
	  
	  ( ctrl + p  + q)
	  ```
	  
	  
		
2.	Busy Box 2

	  ```
	  docker run --name  cbb20  --link cbb10:cbb10-cbb20alias     -it     busybox
	  
	  (cbb10-cbb20alias is link alias name)
	  ```		
		
3.	Testing Connection  

      ```
	  From interactive shell of cbb20 
	  
	  # ping cbb10
	  
	  
	  ( ctrl + p  + q)
	  
	  docker exec -it cbb10
	  
	  # ping cbb20
      ```	  
		
#### Use case : Creating development environment using docker (MySQL + Wordpress)

1.  Remove all containers

      ```
	  docker rm  -f  $(docker ps -aq)
	  
	  docker ps 
	  ```


2.	MySql

      `docker run --name mydb  -d  -e  MYSQL_ROOT_PASSWORD=mysamplepassword  mysql:5`

3.  Wordpress
      
	  ```
	  docker run  --name mywp  -d  -p 5050:80 --link mydb:mydb-mywplink  wordpress
	  
	  
	  validate word press installation 
	  
      Open browser
	  
      <public_ip_of_ec2>:5050
      
	  Eg : 
	  18.138.58.3:5050
	  ```
	  
4.	Verfication 
    
      ```
	   docker inspect -f "{{ .HostConfig.Links }}" mywp
	   
	    "Links": [
                "/mydb:/mywp/mydb-mywplink"
            ]
      ```	
	  
#### Use case : Create LAMP  Architecture using docker [L - Linux , A - ApacheTomcat , M - MySql , P -  Php]	

		( Linux os we already have )
		
1.  Remove all containers

      ```
	  docker rm  -f  $(docker ps -aq)
	  
	  docker ps 
	  ```
	  
2.  To start mysql as container

      `docker run --name mydb  -d  -e  MYSQL_ROOT_PASSWORD=mypass  mysql:5`


3.  To start tomcat as container and link to mysql

      `docker run  --name  myapache  -d  -p 6060:8080  --link mydb:mydb-myapache-link1  tomee`


4.  To see the list of containers

	  `docker container ls`

5.  To check if tomcat is linked with mysql
	  
	  ```
	   docker inspect -f "{{ .HostConfig.Links }}" myapache
	   
	    "Links": [
                "/mydb:/myapache/mydb-myapache-link1"
            ]
      ```	

6.  To start php as container

      `docker  run --name myphp  -d --link myapache:tomcat  --link mydb:myapache-myphp-link1    php`
	  