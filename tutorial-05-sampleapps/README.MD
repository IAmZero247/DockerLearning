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

###  <ins>SpringBoot App</ins>

1. Spring Boot App Git Repo URL : `https://github.com/IAmZero247/spring-boot-docker-app.git`

2. #### <ins>install git client s/w</ins>
`$ sudo yum install git`

3. #### <ins>install maven s/w</ins>
`$ sudo yum install maven`

4. #### <ins>Clone Git Repo</ins>
`$ git clone https://github.com/IAmZero247/spring-boot-docker-app.git`

5. #### <ins>Navigating to project folder</ins>
`$ cd spring-boot-docker-app`

6. #### <ins>Execute maven goals</ins>
`$ mvn clean package`

Note: After package got success, we can see project jar file in target folder.

#### <ins>Create docker image</ins>
`$ docker build -t sb-app .`

#### <ins>Run docker image with port mapping</ins>
`$ docker run -p 8080:8080 sb-app`

Note: Enable 8080 port number in EC2 VM security group

URL To Access Application :   `http://ec2-vm-public-ip:8080/welcome/Ruby`


