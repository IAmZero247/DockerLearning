# Docker Tutorial 03   





### <ins>Dockerfile</ins>
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

####  <ins>FROM</ins>
1.   FROM keyword is used represent base image to create our our image

2.   On Top of base image our image will be created

```
	Syntax: 

	FROM java:jdk-1.8
	FROM tomcat:9.5
	FROM mysql:6.8
	FROM python:3.3	
```	


####  <ins>MAINTAINER</ins>

1.  MAINTAINER keyword is used to specify Dockerfile author information
```
	Syntax:

	MAINTAINER  Zero <ruby4eyes@gmail.com>
```



####  <ins>COPY</ins>


    COPY command is used to copy the files from source to destination while creating docker image

```
	Syntax:

	COPY <source-location>  <destination-location>

	Ex: 

	COPY  target/sbi-app.war   /app/tomcat/webapps/sbi-app.war
```



####  <ins>ADD</ins>


1.  ADD command is also used to copy files from source to destination while creating docker image

```
	Syntax:

	ADD <source-location>  <destination-location>

	ADD <url>  <destination-location>

	Ex: 

	ADD  <URL>   /app/tomcat/webapps/sbi-app.war
```

#### Q: What is the difference between COPY and ADD commands ?

1. Using COPY command we can just copy the files from one path to another path with in the machine

2. Using ADD command we can copy files from one path to another path and it supports source location as URL also.


####  <ins>RUN</ins>


1. RUN instructions will execute while creating the image

2. Using RUN we can give instructions to docker to execute linux commands

3. We can write multiple RUN instructions, docker will process all the RUN instructions from top to bottom

```
Example:

	RUN yum install maven
	RUN yum install git 
	RUN git clone repo-url
	RUN mvn clean package
```


####  <ins>CMD</ins>


1. CMD instructions will execute while creating the container

2. Using CMD command we can run our application package file jar / war file

3. If we write multiple CMD instructions also docker will process only last CMD instruction. There is no use of writing multiple CMD instructions in one Dockerfile.


```
Example:


CMD  sudo start tomcat
```

####  Q: What is the difference between RUN and CMD in Dockerfile ?

1.  RUN is used to execute instructions while creating image

2.  CMD is used to execute instruction while creating Container

3.  We can write multiple RUN instructions in Dockerfile, docker will process all those instructions one by one.

4.  If we write multiple CMD instructions in Dockerfile, docker willl process only last CMD instruction.



####	 <ins>ENTRYPOINT</ins>


1. ENTRYPOINT instructions will execute while creating container

```
	Syntax:

	ENTRYPOINT [ "echo"  , "Welcome to Ashok IT" ]

	ENTRYPOINT [  "java" , "-jar" , "target/boot-app.jar"  ]
```

#### Q: What is the difference between CMD and ENTRYPOINT ?

1. We can override CMD instructions in runtime while creating container

2. We can't override ENTRYPOINT instructions


####  <ins>WORKDIR</ins>


1. It is used to set working directory for an image / container

2. The Dockerfile instructions which are available after WORKDIR  those instructions will be processed from given working directory.

```
	Example: 

	WORKDIR     /app/
```


####   <ins>ENV</ins>


1. ENV is used to set Environment Variables

```
	Example:

	ENV <key> <value>

	ENV   java   /etc/softwares/java
```



####  <ins>ARG</ins>


1.  It is used to remove hard coded values

2.  Using ARG we can pass values in the runtime like below

```
Example:

ARG branch

RUN git clone -b $branch <repo-url>

Useage:

$ docker build -t imageone --build-arg branch=master
```


####  <ins>USER</ins>


1.  We can set user for creating image / container

2.  After USER instruction all the remaining commands will execute with given user permissions



#### <ins>EXPOSE</ins>


1. It is used to specify our container running PORT

2. It is just like a documentation command to provide container running port number.

```
Example: 

EXPOSE 8080
```

 

####  <ins>VOLUME</ins>


1. VOLUME is used to specify docker container data storage location.

2. Volumes are used for storage.


###  <ins>Lab</ins>


```
FROM ubuntu

MAINTAINER Zero<ruby4eyes@gmail.com>

RUN echo "Hi, i am RUN-1"

RUN echo "Hi, i am RUN-2"

CMD echo "Hi, I am CMD-1"

RUN echo "Hi, i am RUN-3"

CMD echo "Hi, i am CMD-2"

```

1. Save the above content in docker file

			default-filename : Dockerfile
2.  Command to create docker image using dockerfile

```
    Syntax :   $ docker build  -t  <image-name>  .

    Ex :   $ docker build  -t  myfirstimage  .
```  
3.  Command to run docker image

```
    $ docker run myfirstimage 
```

4.  We can use customized name  for the dockerfile. When we change dockerfile name we need to pass filename as input for docker build command using -f option like below.
   
```
   $ docker build -f <dockerfile-name>  -t <image-name> .
```	
   
5.  Command to login with dockerhub account

```
		$ docker login
``` 
Note: We need to enter our dockerhub account credentials correctly (it will ask only first time)

6.  Command to tag our docker image

```
	$ docker tag  <image-name>  <tag-name>

	Ex:  $ docker tag myfirstimage ruby4eyes/myfirstimage
```

7.  Command to push docker image to docker hub account

```
	$ docker push <tag-name>
	 
	$ docker push  ruby4eyes/myfirstimage
```

8.  Delete all unused images and stopped containers

```
	$ docker system prune -a
```

9.  Pull the image from docker hub

```
	$ docker pull ruby4eyes/myfirstimage
```

10. Run the image

```
	$ docker run ruby4eyes/myfirstimage 
```