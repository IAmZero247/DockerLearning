####  COPY


    COPY command is used to copy the files from source to destination while creating docker image

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

### Q: What is the difference between COPY and ADD commands ?

1. Using COPY command we can just copy the files from one path to another path with in the machine

2. Using ADD command we can copy files from one path to another path and it supports source location as URL also.


###  RUN


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


###  CMD


1. CMD instructions will execute while creating the container

2. Using CMD command we can run our application package file jar / war file

3. If we write multiple CMD instructions also docker will process only last CMD instruction. There is no use of writing multiple CMD instructions in one Dockerfile.


```
Example:


CMD  sudo start tomcat
```

###  Q) What is the difference between RUN and CMD in Dockerfile ?

1.  RUN is used to execute instructions while creating image

2.  CMD is used to execute instruction while creating Container

3.  We can write multiple RUN instructions in Dockerfile, docker will process all those instructions one by one.

4.  If we write multiple CMD instructions in Dockerfile, docker willl process only last CMD instruction.




