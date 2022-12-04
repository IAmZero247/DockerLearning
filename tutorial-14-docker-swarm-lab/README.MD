# Docker Tutorial 10 - Docker Swarm Lab

1. In Docker swarm we need to deploy our application as a service.

## <ins>Docker Swarm Service</ins>

1. Service is collection of one or more containers of same image

2. There are 2 types of services in docker swarm

	1. Replica (default mode)
	2. global


3. Syntax
  ```
  
  $ sudo docker service create --name <serviceName> -p <hostPort>:<containerPort> <imageName>
  
  Ex :  $ sudo docker service create --name sb-app -p 8080:8080 ruby4eyes/sb-app
  
  ```



4. By default 1 replica will be created


### <ins>Check the services created</ins>
`$ docker service ls` 

### <ins>We can scale docker service</ins>
```
$ docker service scale <serviceName>=<no.of.replicas>

$ docker service scale sb-app=4 
```

### <ins>Check the services created</ins>
`$ docker service ls` 

```
ID             NAME      MODE         REPLICAS   IMAGE                     PORTS
dvlkuzr46h2p   sb-app    replicated   4/4        ruby4eyes/sb-app:latest   *:8080->8080/tcp
```

### <ins>Inspect docker service</ins>
`$ sudo docker service inspect --pretty <service-name>`

```
ID:             dvlkuzr46h2p7sks517ubtymi
Name:           sb-app
Service Mode:   Replicated
 Replicas:      4
Placement:
UpdateConfig:
 Parallelism:   1
 On failure:    pause
 Monitoring Period: 5s
 Max failure ratio: 0
 Update order:      stop-first
RollbackConfig:
 Parallelism:   1
 On failure:    pause
 Monitoring Period: 5s
 Max failure ratio: 0
 Rollback order:    stop-first
ContainerSpec:
 Image:         ruby4eyes/sb-app:latest@sha256:5e3cd5ff6532936698e54f6adffbc55db5543c81badd1dd605beb0f81e82c5b3
 Init:          false
Resources:
Endpoint Mode:  vip
Ports:
 PublishedPort = 8080
  Protocol = tcp
  TargetPort = 8080
  PublishMode = ingress

```

### <ins>See service details</ins>
`$ sudo docker service ps <service-name>`

```
$ sudo docker service ps sb-app

ID             NAME       IMAGE                     NODE               DESIRED STATE   CURRENT STATE           ERROR     PORTS
n3eg29r2goo6   sb-app.1   ruby4eyes/sb-app:latest   ip-172-31-88-166   Running         Running 5 minutes ago
82ac9bsonzmj   sb-app.2   ruby4eyes/sb-app:latest   ip-172-31-80-236   Running         Running 3 minutes ago
omb6oqkcdpy1   sb-app.3   ruby4eyes/sb-app:latest   ip-172-31-80-236   Running         Running 3 minutes ago
levim5gpdvhn   sb-app.4   ruby4eyes/sb-app:latest   ip-172-31-90-61    Running         Running 3 minutes ago

```

### <ins>Remove one node from swarm cluster</ins>
`$ sudo docker swarm leave`

### <ins>Remove docker service</ins> 
`$ sudo docker service rm <service-name>`


