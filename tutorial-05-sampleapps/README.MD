# Docker Tutorial 05   





### <ins>Dockerfile</ins>
1.  Dockerfile contains instructions to build docker image

2. Below are the Dockerfile Keywords

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

###  <ins>Dockerizing SpringBoot App</ins>

1. Spring Boot App Git Repo URL : `https://github.com/IAmZero247/spring-boot-docker-app.git`

    1. Spring Boot is one ready made java based framework available in the market to develop java based applications quickly
	2. Spring Boot is providing emedded server (internal server will be available, we no need to configure server for execution)
	3. Spring Boot application will be packaged as jar file  (mvn clean package goal will do that package)
	4. Note:  When we do maven package, project jar will be created in project target folder
	5. To run spring boot applications we just need to run  jar file like below
       `$  java -jar <boot-app-jar-file>`
	6. Docker File   
	   ```
	    FROM openjdk:11

		COPY target/spring-boot-docker-app.jar  /usr/app/

		WORKDIR /usr/app/

		ENTRYPOINT ["java", "-jar", "spring-boot-docker-app.jar"]
	   ```


2. #### <ins>Install git client s/w</ins>
	`$ sudo yum install git`

3. #### <ins>Install maven s/w</ins>
	`$ sudo yum install maven`

4. #### <ins>Clone Git Repo</ins>
	`$ git clone https://github.com/IAmZero247/spring-boot-docker-app.git`

5. #### <ins>Navigating to project folder</ins>
	`$ cd spring-boot-docker-app`

6. #### <ins>Execute maven goals</ins>
	`$ mvn clean package`

    1. Note: After package got success, we can see project jar file in target folder.

7. #### <ins>Create docker image</ins>
	`$ docker build -t sb-app .`

8. #### <ins>Tag Image and push to docker hub</ins>
	```
	$ docker tag sb-app ruby4eyes/sb-app
	$ docker push ruby4eyes/sb-app
	```

9. #### <ins>Pull image from docker hub</ins>
	```
	$ docker system prune -a	
    $ docker pull ruby4eyes/sb-app
	```

10. #### <ins>Run docker image with port mapping</ins>
	`$ docker run -p 8080:8080 sb-app`
	
	`$ docker run -d -p 8080:8080 ruby4eyes/sb-app `

	1.	Note: Enable 8080 port number in EC2 VM security group

	2.	URL To Access Application :   `http://ec2-vm-public-ip:8080/welcome/Ruby`

11. 	#### <ins>We can check logs of the container using below command</ins>
     `$ docker logs <container-id>`
	 	 
###  <ins>Dockerizing Java Web Application (Without SpringBoot)</ins>

1. Java Web App Git Repo URL : `https://github.com/IAmZero247/java-maven-web-app.git`
   1. Java web applictaions will be packaged as warIAmZero247file
   2. WAR (Web Archive) contains application code
   3. To run the war file we need webserver (Ex: Apache Tomcat)
   4. We need to deploy war file in Tomcat Server for Execution
   5. In Tomcat server we will have "webapps" folder for deployment
   6. Note: To run normal java web applications we need  "java & tomcat" as dependencies
   7. Docker File   
	   ```
	    FROM tomcat:8.0.20-jre8

		COPY target/01-maven-web-app.war   /usr/local/tomcat/webapps/maven-web-app.war
	   ```
	   
2. `$ git clone https://github.com/IAmZero247/java-maven-web-app.git`

3. `$ cd java-maven-web-app`

4. `$ mvn clean package`

5. `$ docker build -t java-maven-web-app .`

6. `$ docker tag java-maven-web-app ruby4eyes/java-maven-web-app`

7. `$ docker push ruby4eyes/java-maven-web-app`

8. `$ docker images`

9. `$ docker run -d -p 8080:8080 java-maven-web-app`

10. `$ docker ps`

11. `$ docker logs <container-id>`


12. URL To access The Application :  `http://ec2-vm-public-ip:host-port/maven-web-app`
    1. Note: In the above url "maven-web-app" is called as context path (name of the war file will become context path)
	

###  <ins>Dockerizing Python Flask App</ins>	

1. Python Flask app Git Repo URL: https://github.com/IAmZero247/python-flask-docker-app.git
    1. Python is a general purpose scripting language
	2. Python programs will have .py as extension
    3. Compilation is not required for python programs
	4. Docker File   
	   ```
		FROM python:3.6

		MAINTAINER ZR "ZR@gmail.com"

		COPY . /app

		WORKDIR /app

		EXPOSE 5000

		RUN pip install -r requirements.txt

		ENTRYPOINT ["python", "app.py"]
	   ```
2. `$ git clone https://github.com/IAmZero247/python-flask-docker-app.git`

3. `$ cd python-flask-docker-app`

4. `$ docker build -t python-flask-app .`

5. `$ docker images`

6. `$ docker run -d -p 5000:5000 python-flask-app`

7. `$ docker ps`

8. `$ docker logs <container-id>` 


9. #### <ins>Command to enter into docker container</ins>
   `$ docker exec -it <container-id> /bin/bash`

   1. Note: Execute 'exit' command to come out from docker container vm.
	   
	   
