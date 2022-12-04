# Docker Tutorial 10 - Docker Swarm  

1. <ins>Docker :</ins> It is a containerization platform. It is used to deploy the applications as containers.

2. <ins>Docker Swarm :<ins> It is an Orchestration Platform. It is used to manage docker containers.

   1. Managing docker containers nothing but creating / updating / scale up / scale down / remove containers

   2. In market we have docker swarm, kubernetes, open shfit as Orachestration platforms.


3. Docker Swarm is used to setup Docker Cluster

   1. Cluster means group of servers

   2. Docker swarm is embedded in Docker engine ( No need to install Docker Swarm Seperatley )

   3. We will setup Master(Manager) and Worker nodes using Docker Swarm cluster

   4. Master(Manager) Node  will schedule the tasks (containers) and manage the nodes and node failures

   5. Worker nodes will perform the action (containers will run here) based on master node instructions


## <ins>Swarm Features</ins>

1. Cluster Management
2. Decentralize design
3. Declarative service model
4. Scaling
5. Multi Host Network
6. Service Discovery
7. Load Balancing
8. Secure by default
9. Rolling Updates


## <ins>Docker Swarm Cluster Setup In Aws </ins>


1. #### Create 3 EC2 instances (ubuntu) & install docker in all 3 instances using below 2 commands
	```
		$ curl -fsSL https://get.docker.com -o get-docker.sh
		$ sudo sh get-docker.sh
	```
	1. Note: Enable 2377 port in security group for Swarm Cluster Communications
    2. Note: SSH user is ubuntu
    3. Now we can choose one as Manager node and other 2 as Worker nodes



2. #### Connect to Master Machine and execute below command [Initialize docker swarm cluster]

   `$ sudo docker swarm init --advertise-addr <private-ip-of-master-node>`

    1. Ex : $ sudo docker swarm init --advertise-addr 172.31.37.100

3. #### Get Join token for worker from master  (this token is used by workers to join with master)
   `$ sudo docker swarm join-token worker`

   1. Note: Copy the token and execute in all worker nodes with sudo permission

   2. Ex: sudo docker swarm join --token SWMTKN-1-4pkn4fiwm09haue0v633s6snitq693p1h7d1774c8y0hfl9yz9-8l7vptikm0x29shtkhn0ki8wz 172.31.37.100:2377

4. #### Incase if we need more managers, We need to use join token for manager 
   `$ sudo docker swarm join-token manager`

## <ins>Q: what is docker swarm manager quarm?</ins>

1. Ans) If we run only 2 masters then we can't get High Availability 


2. Formula : (n-1)/2

	1. If we take 2 servers and one goes down  

			(2-1)/2 => 0.5 ( It can't become master )

			(3-1)/2 => 1 (it can be leader when the main leader is down)

	2. Note: Always use odd number for Master machines


