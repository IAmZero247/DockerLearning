# Docker Tutorial 03   





### Dockerfile
1.  Dockerfile contains instructions to build docker image

2.  In Dockerfile we will use DSL (Domain Specific Language) keywords

3.  Docker engine will process Dockerfile instructions from top to bottom

4.  Below are the Dockerfile Keywords

    ```
	        1.  FROM
		2.  MAINTAINER
		3.  COPY
		4.  ADD
		5.  RUN
		6.  CMD
		7.  ENTRYPOINT
		8.  ENV
		9.  LABEL
		10. WORKDIR
		11. EXPOSE
		12. VOLUME
    ```	

####  FROM
1.   FROM keyword is used represent base image to create our our image

2.   On Top of base image our image will be created

```
	Syntax: 

	FROM java:jdk-1.8
	FROM tomcat:9.5
	FROM mysql:6.8
	FROM python:3.3	
```	


####  MAINTAINER

1.  MAINTAINER keyword is used to specify Dockerfile author information
```
	Syntax:

	MAINTAINER  Zero <ruby4eyes@gmail.com>
```



####  COPY


2.  COPY command is used to copy the files from source to destination while creating docker image

```
	Syntax:

	COPY <source-location>  <destination-location>

	Ex: 

	COPY  target/sbi-app.war   /app/tomcat/webapps/sbi-app.war
```



####  ADD


1.  ADD command is also used to copy files from source to destination while creating docker image

```
	Syntax:

	ADD <source-location>  <destination-location>

	ADD <url>  <destination-location>

	Ex: 

	ADD  <URL>   /app/tomcat/webapps/sbi-app.war
```

2.  What is the difference between COPY and ADD commands ?

a. Using COPY command we can just copy the files from one path to another path with in the machine

b. Using ADD command we can copy files from one path to another path and it supports source location as URL also.



* If you do not specify the version, by default, we get latest version 

	  
1.	To download Tomcat 

      `docker pull tomee`
		
2.	To download ubuntu

      `docker pull ubuntu`		
		
3.	To download jenkins 

      `docker pull jenkins/jenkins` 
		
4.	Create a container from image  

      `docker run --name mytomcat  -p   7070:8080   tomee` 
	  
	  ```
	  verify using private ip of ec2:
	  
	  http://13.250.47.90:7070
	  ```
	  
5.	Stop the container 

      `docker stop  mytomcat` 
	  
6.	Remove the container 

      `docker rm -f mytomcat` 
	  
7.	Run container in detached mode  

      `docker run --name   mytomcat  -p 7070:8080   -d   tomee` 
	  
			( The above command  runs tomcat in detached mode , so we get out # prompt back )
	  
8.	Run jenkins container and verify  

      `docker run --name myjenkins  -p 9090:8080    -d   jenkins/jenkins`
	  
      ```
	  verification:
	  
	  http://13.250.47.90:9090
	  ```	  
	  
9.	Run ubuntu container in IT  

      `docker run   --name myubuntu   -it   ubuntu`
	  
	  ```
	  Observation:  You have automatically entered into ubuntu
		# ls  ( To see the list of files in ubuntu )
		# exit  ( To comeout of container back to host )
      ```

	  
	  
	  
	  
	  
		  
		  
### Scenario 1: Start centos as container 

  `docker run --name mycentos  -it  centos`
	  
  `exit  ( To come back to dockerhost )`
		
### Scenario 2: Start tomcat as a container and name it as "webserver". Perform port mapping and run this container in detached mode

  `docker run --name webserver -p 7070:8080  -d tomee`
	  
  ```
  To access homepage of the tomcat container
  Launch any browser
  <public_ip_of_dockerhost>:7070
  ```

### Scenario 3: Start jenkins as a container in detached mode , name is as "devserver", perform port mapping

  `docker run -d  --name  devserver  -p 9090:8080 jenkins/jenkins`
      
  ```
  To access home page of jenkins ( In browser)
  <public_ip_of_dockerhost>:9090
  ```

### Scenario 4: Start nginx as a container and name as "appserver", run this in detached mode ,   perform automatic port mapping 

  `docker run --name  appserver  -P  -d  nginx`
	  
				( if image is not available, it perform pull operation automatically )
				( Capital P  , will perform automatic port mapping )
	  
  ```
  How to check nginx is running or not?
	  
  To know the port that is reserved for nginx 
	  
	  1. docker port  appserver
        80/tcp -> 0.0.0.0:32768
		
		80  is nginx port
		32768  is  dockerhost port
		
		or
		
	  2. docker container ls    ( to see the port of nginz and docker host )
  ```
	  
  ```
  verification:  check nginx on browser
  52.221.192.237:32768
  ```

### Scenario 5: To start mysql  as container, open interactive terminal in it, create a sample table.

  `docker run  --name  mydb  -d  -e MYSQL_ROOT_PASSWORD=mypassword  mysql:5`
	  
  ```
  1. docker container ls
	  
  2. open container in Interactive Shell:
	  
    docker  exec   -it  mydb  bash
  ```
	  
  ```
  1. To connect to mysql database
		
	mysql  -u  root  -p 
		 
  2. Enter the password, we get mysql  prompt
	  
  3. To see list of databases

	> show databases;
		
  4. To switch to a databse
		
	> use db_name
        
	Eg:
	
	> use mysql;

  5. To create emp tables and dept tables use below def 
		
	https://justinsomnia.org/2009/04/the-emp-and-dept-tables-for-mysql/
		
  6. Verify 
  
    > show tables; 
	   
  7. Exit 	   
	   
 	> exit
	# exit
	# exit
			
  ```		

	  
