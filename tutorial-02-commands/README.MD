# Docker Tutorial 02  





### Image Commands 

	  
1.	To download a docker image 

      `docker pull image_name`
		
      ```
	  docker pull tomee
      docker pull ubuntu
      docker pull jenkins/jenkins
	  ```
		
2.	To see the list of docker images 

	  ```
	  docker image ls 
		(or) 
	  docker images
      ```		
		
3.	To delete a docker image from docker host 

      `docker rmi image_name/image_id` 
		
4.	To upload a docker image into docker hub 

      `docker push image_name` 
	  
5.	To tag an image 

	  `docker tag   image_name   ipaddress_of_local_registry:5000/image_name` 
	  
6.	To build an image from a customised container 

      `docker   commit  container_name/container_id     new_image_name` 
	  
7.	To create an image from docker file 

      `docker build -t    new_image_name` 
	  
8.	To search for a docker image 

      `docker search image_name` 
	  
9.	To delete all images that are not attached to containers 

      `docker system prune -a` 
	  
	  
		  
		  

		
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

