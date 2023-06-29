----------Self Exam----------

Docker server that runs a web app with db, SSL and cache

----------requirements----------

	runs on nginx - V
	uses WordPress not Apache version - V
	has mysql db - V
	works with SSL - V
	domain set - V
	had redis cache with php plugin - V

----------notes----------

	1. docker works by packaging the application with all the dependencies in a single place 
	to make the program run the same on every platform
	2. docker has a client-server architecture
	3. the docker engine is the client-server in the docker deployment structure
	4. every docker container is separated and not affected by any other container
	5. docker uses images to create instances (containers) of a program/app
	6. docker images stored in the registry (mostly hub.docker.com) 
	7. docker images have tags that specify different types of the same image
	8. creation of custom docker images is made with a docker file

----------docker differnet from a vm----------
   
 ----------vm----------
	
	 need a set amount of system resources for each VM
	 need hypervisor
	 lot more resource-heavy than a container
	 not so scaleable
	 can perform differently on each system
	 structure - 
	 	host os -> hypervisor -> guest os -> app
		
 ----------Docker----------
	
	 isolated	
	 lightweight
	 portable
	 works in the deployment stage
	 makes every program run the same on any system
	 very scaleable
	 docker containers will work identically on each system
	 structure - 
	 	host os -> (VM is optional here) -> container engine -> filesystem -> app

----------good to know----------

	Dockerfile - text file with instructions to build an image (automation of docker image creation)
	Docker image - template used to create Docker containers
	Docker container - running instance of an image
	Docker image tag - image version or type
	Docker daemon - use of docker images and containers together
	Docker engine - the communication between the docker client-server to perform tasks
	Dangling image - Docker image that is associated with a running container

----------Docker compose----------

----------notes----------

	1. use 2 spaces not tabs in the docker-compose.yml file
	2. not recommended to forward port to the same port in web apps (80:80/443:443 is bad and can clash with other services)
	3. docker-compose has a full network that can be configured example: bridged (driver)

 ----------template----------

	version: ''
	  services:
	    [ServiceName]:
	      image:[imageName:tag]/build:[DockerfilePath]
	      container_name: [name of container]
	      env_file:
	        -.env
	      volumes:
	        - [pathOnHost]:[pathToMount]
	      ports:
	        - [hostPort]:[dockerPort] 
	      environment:
	        - [environmentVar]=[value]
	      networks:
	        - [networkName]
	      command: [commandToRunOnStartup]
	      depends_on:
	        - [nameOfDependedOnContainer]
	      restart: (unless-stopped/always)
	  networks:
	    [DockerNetworkName]:
	      name: [name]
	      driver: [type]

----------commands-----------

Basic

	: docker version
	: docker -v
	: docker info
	: docker --help
	: docker login

Images

	: docker images --help
	: docker pull image
	: docker images
	: docker images -q
	: docker images -f “dangling=false”
	: docker images -f “dangling=false” -q
	: docker run image
	: docker rmi image
	: docker rmi -f image
	: docker inspect
	: docker history imageName

Containers

	: docker ps
	: docker run ImageName
	: docker start ContainerName/ID
	: docker stop ContainerName/ID
	: docker pause ContainerName/ID
	: docker unpause  ContainerName/ID
	: docker top ContainerName/ID
	: docker stats ContainerName/ID
	: docker attach ContainerName/ID
	: docker kill ContainerName/ID
	: docker rm ContainerName/ID
	: docker history ImageName/ID
 
System

	: docker stats
	: docker system df
	: docker system prune
 
Dockerfile

	: infile commands(FROM,RUN,CMD)
	: docker build 
	: docker build -t ImageName:Tag directoryOfDocekrfile
	: docker run image
	 
Compose

	: docker-compose up --force-recreate -d
	: docker container rm -f $(docker container ls -q)
	: docker images rm $(docker images ls -q)
