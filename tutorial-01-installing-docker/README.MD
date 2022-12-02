# Docker Tutorial 01 - Installing Docker + Docker Terminologies 





### Installing Docket in AWS 
1.	Create Ubuntu Machine on AWS
	  * { All Traffic – anywhere }
		   
2. 	Connect using git bash and go to Root Account

      * $ sudo  su –
			
3.	Download and run shell script

      * https://get.docker.com/
		   
            ```
			curl -fsSL https://get.docker.com -o get-docker.sh`
            sh get-docker.sh
            ```
			
4.	Verify Docker Installation 

      * docker --version
		  
		  
### Docker Terminologies 
    1. Dockerfile
    
      	Dockerfile contains set of instructions to build docker image. In dockerfile we will specify which sotwares are required to run our code/application.
   
    2. Docker Images   
	
		Combinations of binaries / libraries  + application code which are necessary for one software application.
		
    3. Docker Containers  
	
		When image is installed and in comes into running condition, it is called container. 
		
		Docker container is runtime instance of our application. When we run Docker Image it will create Docker Container. Inside Container our application and application dependencies will be available.
		
    4. Docker Host
	
		Machine on which docker is installed, is called as Docker host.
		
    5. Docker Client
	
		Terminal used to run docker run commands ( Git bash )
    
    6. Docker Registry
    
    	Docker Registry is a place which is used to store docker images for future purpose 

		Ex: Docker Hub, Amazon ECR etc....
		
### Verify the docker install with

`docker run hello-world`		


### Running an ubuntu container in foreground mode (interactive shell mode)

`docker run -it ubuntu bash`

```
-t              : Allocate a pseudo-tty
-i              : Keep STDIN open even if not attached
```

### Running an nginx container in background mode (detach mode) and mapping a port

`docker run -d -p 8080:80 nginx`

```
-d=false: Detached mode: Run container in the background, print new container id
-p=[]      : Publish a container's port or a range of ports to the host
               format: ip:hostPort:containerPort | ip::containerPort | hostPort:containerPort | containerPort
               Both hostPort and containerPort can be specified as a
               range of ports. When specifying ranges for both, the
               number of container ports in the range must match the
               number of host ports in the range, for example:
                   -p 1234-1236:1234-1236/tcp

               When specifying a range for hostPort only, the
               containerPort must not be a range.  In this case the
               container port is published somewhere within the
               specified hostPort range. (e.g., `-p 1234-1236:1234/tcp`)

               (use 'docker port' to see the actual mapping)
```

### Show the running containers

`docker ps`

### Stopping a running container

`docker stop CONTAINER_ID`

### Resources

* [Docker Reference - run](https://docs.docker.com/engine/reference/run/)
* [Docker Reference - ps](https://docs.docker.com/engine/reference/commandline/ps/)
* [Docker Reference - stop](https://docs.docker.com/engine/reference/commandline/stop/)
