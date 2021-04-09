# Docker Tutorial 04 - Multi container architecture using docker   

1. --link
2. docker-compose

## Link
------- 

#### Use case : Start two busybox containers and create link between them 

 

	  
1.	Busy Box 1 

      `docker run --name cbb10 -it   busybox`
	  
	  ```
	  To exit from INTERACTIVE SHELLL of a container 
	  
	  ( ctrl + p  + q)
	  ```
	  
	  
		
2.	Busy Box 2

	  ```
	  docker run --name  cbb20  --link cbb10:cbb10-cbb20alias     -it     busybox
	  
	  (cbb10-cbb20alias is link alias name)
	  ```		
		
3.	Testing Connection  

      ```
	  From interactive shell of cbb20 
	  
	  # ping cbb10
	  
	  
	  ( ctrl + p  + q)
	  
	  docker exec -it cbb10
	  
	  # ping cbb20
      ```	  
		
#### Creating development environment using docker (MySQL + Wordpress)

1.	MySql

      `docker run --name mydb  -d  -e  MYSQL_ROOT_PASSWORD=mysamplepassword  mysql:5`

2.  Wordpress
      
	  ```
	  docker run  --name mywp  -d  -p 5050:80 --link mydb:mydb-mywplink  wordpress
	  
	  
	  validate word press installation 
	  
      Open browser
	  
      <public_ip_of_ec2>:5050
      
	  Eg : 
	  18.138.58.3:5050
	  ```	  
	  
#### Create LAMP  Architecture using docker [L - Linux , A - ApacheTomcat , M - MySql , P -  Php]	

		( Linux os we already have )