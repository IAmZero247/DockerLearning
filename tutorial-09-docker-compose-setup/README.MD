# Docker Tutorial 09 - Multi Container Architecture Using Docker   

1. link (adhoc way)
2. docker-compose

## <ins>Docker Compose</ins>

1. In Microservices Application , Application functionality will be developed as micro services (rest apis). Every functionality will be developed as individual project (individual API)
2. Every API should run in a seperate container
3. Running Multiple containers manully for all the apis is difficult job
4. To solve this problem Docker-Compose came into picture
5. Docker Compose is a tool which is used to manage multi container based applications
6. Using Docker Compose we can easily setup & deploy multi container based applications
7. We will give containers information to Docker Compose using YML file  (docker-compose.yml)
8. Docker Compose YML should have all the information related to containers creation
9. Structure of docker compose file
```
	======================
	Docker Compose YML File
	======================

	version:

	services:

	network:

	volumes:

	=====================
```

10.  Docker Compose default file name is  "docker-compose.yml"

#### <ins>Create Containers using Docker</ins>
`$ docker-compose up`

#### <ins>Create Containers using Docker Compose with custom file name</ins>
`$ docker-compose -f <filename> up`

#### <ins>Display Containers created by Docker Compose</ins>
`$ docker-compose ps`

#### <ins>Display docker compose images</ins>
`$ docker-compose images`

#### <ins>Stop & remove the containers created by docker compose</ins>
```
$ docker-compose stop
$ docker-compose down   --> this will remove volumes to 
```
### <ins>Docker Compose Setup</ins>

	  
1.	Open https://docs.docker.com/compose/install/ 
	  
		
2.	Go to linux section Copy and pase the below two commands

	  ```
	  # sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
	  
	  # sudo chmod +x /usr/local/bin/docker-compose
	  
	  Creating symbolic link
	  # sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
	  ```		
		
3.	Verification

      `docker-compose  --version`	  
		
### <ins>Validate YAML</ins>

1.  Open  http://www.yamllint.com/

      * Paste YAML sample code  
	  * Hit Go button


### Name of the file should be docker-compose.yml

### Use case : Spring Boot with MySQL using Docker Compose [Compose file use networks]

1. ##### Spring Boot App with MySQL DB Git repo URL 
                  
	1. URL : `https://github.com/IAmZero247/spring-boot-mysql-docker-compose.git`

2. ##### Docker-compose file

```
	---
	version: "3"
	services:
	  application:
		image: ruby4eyes/spring-boot-mysql-app
		networks:
		  - springboot-mysqldb-net
		ports:
		  - "8080:8080"
		depends_on:
		  - mysqldb
	  mysqldb:
		image: mysql:5.7
		networks:
		  - springboot-mysqldb-net
		environment:
		  - MYSQL_ROOT_PASSWORD=root
		  - MYSQL_DATABASE=sbms
	networks:
	  - springboot-mysqldb-net:
	...	
```	
3. ##### Clone git repo url
`$ git clone https://github.com/IAmZero247/spring-boot-mysql-docker-compose.git`

4. ##### Get into project directory
`$ cd spring-boot-mysql-docker-compose`

5. ##### Build Maven Project
`$ mvn clean package`

6. ##### Create Docker Image  ( Image Name : spring-boot-mysql-app )
```
	$ docker build -t spring-boot-mysql-app .
	
	$ docker tag spring-boot-mysql-app ruby4eyes/spring-boot-mysql-app
	
	$ docker push ruby4eyes/spring-boot-mysql-app
	
	$ docker system prune -af  
```	

7. ##### Check docker image created or not
`$ docker images`

8. ##### Run /Stop containers using docker compose ( docker-compose.yml available )
```
	$ docker-compose  -f docker-compose-with-mysql.yml up -d
	
	$ docker-compose  -f docker-compose-with-mysql.yml stop
	
	$ docker-compose  -f docker-compose-with-mysql.yml down
	
```
9. ##### Check containers which are created
`$ docker-compose ps`

10. ##### Check logs of application contianer
`$ docker logs -f <container-name>`

 1. Note: Access the application in browser

	URL : http://ec2-vm-public-ip:host-port/


11. ##### Get into App container to check jar file 
`$ docker exec -it <container-name> /bin/bash/`


12. ##### Check DB tables by entering into container
```
	$ docker exec -it <db-container-name> /bin/bash

	$ mysql -u root -p

	$ show databases;

	$ use <db-name>   (our db name is sbms)

	$ show tables;

	$ select * from table-name  (our table name is book)
```






### Use case : Creating development environment using docker (MySQL + Wordpress) [Compose file use links]

1.  Remove all the running container

      `docker rm -f $(docker ps -aq)`

2.  Create docker file
 
      `vim docker-compose.yml`

3.  Paste
    
      ```
	  ---
      version: '3'

      services:
		mydb:
			image: mysql:5
			environment:
			MYSQL_ROOT_PASSWORD: mypass

		mywp:
			image: wordpress
			ports:
			  - 5050:80
            links:
			  - mydb:mysql-wp-l1
      ---

	  :wq
      ```	

4.  Start above services from dockerfile 

      `docker-compose  up`
	  
5.  Stop above services 
    
      `docker-compose stop`	
	  
6.	Start services in detached mode 

      ```
	  
      docker rm -f $(docker ps -aq)                  		[remove all running containers]
	  
	  docker-compose up  -d
	  
      ```
7.  Validate wordpress 

      `public_ip:5050`	  
	
	  ```
	
	  docker inspect -f "{{ .HostConfig.Links }}" mywp
 
      "Links": [
          "/mydb:/mywp/mysql-wp-l1"
      ]
	  
	  ```  
	  
	  