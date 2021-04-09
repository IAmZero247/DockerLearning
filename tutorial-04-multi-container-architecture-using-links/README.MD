# Docker Tutorial 04 - Multi Container Architecture Using Docker   

1. link (adhoc way)
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

6.  To start php as container (link with mydb && )

      `docker  run --name myphp  -d --link myapache:myapache-myphp-link1  --link mydb:mydb-myphp-link1    php`

#### Use case : Create CI-CD environment, where jenkins container is linked with two Tomcat containers.

1.  Remove all containers

      ```
	  docker rm  -f  $(docker ps -aq)
	  
	  docker ps 
	  ```
	  
2.  Jenkin Server 

      `docker run  --name  jenkin1  -d -p 7070:8080 jenkins/jenkins`	
	
	  ```
	  To check jenkins is running or not?
	
	  Open browser
	
	  public_ip:7070
      Eg: http://18.138.58.3:7070
	  ```

3.  Dev Server 

      `docker run --name  devserver  -d  -p 8080:8080 --link jenkin1:j-dev1 tomee`	
	
	  ```
	  To check the Tomcat use public_ip but port number will be 8080
	  
      http://18.138.58.3:8080
	  ```
4.  Prod Server	  

      `docker run --name  prodserver  -d  -p 9090:8080 --link jenkin1:j-prod1 tomee`
	  
	  ```
	  To check the Tomcat use public_ip but port number will be 8080
	  
      http://18.138.58.3:9090
	  ```
#### Use case : Create Selenium Hub container, and link it with two node containers. One node with firefox installed, another node with chrome installed.

      * Tester should be able to run selenuim automation programs for testing the application on multiple browsers.

1.  Selenium Hub
    
      `docker run --name  hub  -d -p 4444:4444   selenium/hub`

2.  Selenium Node Chrome

      `docker run --name chrome  -d -p 5901:5900  --link hub:selenium   selenium/node-chrome-debug`
	  
3.  Selenium Node Firefox
	
      `docker run --name chrome  -d -p 5902:5900  --link hub:selenium   selenium/node-firefox-debug`	
	
	
4.  Note: firefox and chrome containers are GUI containers.

      * To see the GUI interface to chrome / firefox container
        ------------------------------------------------------
        Download and install vnc viewer
        
		In VNC viewer search bar
        public_ip_dockerhost:5901
		
		18.136.211.65:5901
        Password - secret
	  