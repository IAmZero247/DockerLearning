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

####  <ins>SpringBoot App</ins>

1. Spring Boot App Git Repo URL : https://github.com/ashokitschool/spring-boot-docker-app.git

2. ###### install git client s/w
$ sudo yum install git

3. ####### install maven s/w
$ sudo yum install maven

4. ###### Clone Git Repo
$ git clone https://github.com/ashokitschool/spring-boot-docker-app.git

5. # Navigating to project folder
$ cd spring-boot-docker-app

6. # execute maven goals
$ mvn clean package

Note: After package got success, we can see project jar file in target folder.

# create docker image
$ docker build -t sb-app .

# run docker image with port mapping
$ docker run -p 8080:8080 sb-app

Note: Enable 8080 port number in EC2 VM security group

URL To Access Application :   http://ec2-vm-public-ip:8080/welcome/Ashok


