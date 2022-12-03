# Docker Tutorial 03   





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

8. #### <ins>Run docker image with port mapping</ins>
	`$ docker run -p 8080:8080 sb-app`
	
	`$ docker run -d -p 8080:8080 ashokit/sb-app `

	1.	Note: Enable 8080 port number in EC2 VM security group

	2.	URL To Access Application :   `http://ec2-vm-public-ip:8080/welcome/Ruby`

9. 	#### <ins>We can check logs of the container using below command</ins>
     `$ docker logs <container-id>`
	 	 
###  <ins>Dockerizing Java Web Application (Without SpringBoot)</ins>

1. Notes
   1. Java web applictaions will be packaged as war file
   2. WAR (Web Archive) contains application code
   3. To run the war file we need webserver (Ex: Apache Tomcat)
   4. We need to deploy war file in Tomcat Server for Execution
   5. In Tomcat server we will have "webapps" folder for deployment
   6. Note: To run normal java web applications we need  "java & tomcat" as dependencies