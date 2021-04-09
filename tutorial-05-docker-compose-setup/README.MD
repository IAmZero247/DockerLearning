# Docker Tutorial 04 - Multi Container Architecture Using Docker   

1. link (adhoc way)
2. docker-compose

## Docker Compose
----------------- 

### Docker Compose Setup

	  
1.	Open https://docs.docker.com/compose/install/ 
	  
		
2.	Go to linux section Copy and pase the below two commands

	  ```
	  # sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
	  
	  #sudo chmod +x /usr/local/bin/docker-compose
	  ```		
		
3.	Verification

      `docker-compose  --version`	  
		
### Validate YAML

1.  Open  http://www.yamllint.com/

      * Paste YAML sample code  
	  * Hit Go button


### Name of the file should be docker-compose.yml


### Use case : Creating development environment using docker (MySQL + Wordpress)

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
	  
	  