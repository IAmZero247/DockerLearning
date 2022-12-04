# Docker Tutorial 08   





### <ins>Docker Networks</ins>
1. Docker network is used to provide isolated network for Docker Containers. Network is all about communications

2. In Docker we will have below 3 default networks

			1. none
			2. host
			3. bridge
			
3. In Docker we have below 5 network drivers

		1. Bridge ----> Default network driver in Docker, bridge driver is recommended driver when we are running standalone container. It will assign one IP for container
		2. Host ----> Host Driver is also used for standalone container. IP will not be assigned for container
		3. None ----> None means no network will be provided by our Docker containers
		4. Overlay  ----> Overlay network driver is used for Orchestration. Docker Swarm will use this Overlay network driver
		5. Macvlan ----> Macvlan driver will assign MAC address for a container. It makes our container as Physical. 




### <ins>Display docker networks available</ins>
`$ docker network ls`

### <ins>Create docker network</ins>
`$ docker network create ruby-sample-network`

### <ins>Inspect network</ins>
`$ docker network inspect <network-name>`

### <ins>Delete docker network</ins>
`$ docker network rm <network-id>`

### <ins>Run a container with given network</ins>
`$ docker run -d -p hport:cport --network ruby-sample-network <imagename>`    
