Contents
- [What is Docker](#_what-is-docker_)
- [Some Basic Terminologies Related to Docker](#some-basic-terminologies-related-to-docker)
- [Some Basic Docker Commands](#_some-basic-docker-commands_)
- [Dockerfile Instructions](#dockerfile-instructions)
- [Manage Data in Docker](#manage-data-in-docker)
- [How to Push Docker Image to Docker Hub](#how-to-push-docker-image-to-docker-hub)

#### _What is Docker_
- Docker is an open-source containerization platform that allows developers to quickly create, deploy and run applications inside 
  containers. These containers allow developers to package up an application with all the parts it needs, such as libraries and
  other dependencies, and ship it all out as one package. By doing so, thanks to the container, the developer can rest assured
  that the application will run on any other Linux machine regardless of any customized settings that machine might have that
  could differ from the machine used for writing and testing the code.


- Traditionally, Applications were deployed on Physical Server or Virtual Machines. But, This approach has several drawbacks
  - Each application was deployed on a separate server or VM. This resulted in `under utilization of resources`.
  - `Portability` of application was a challenge. It was difficult to move application from one server to another.
  - `Boot up` time was high. It took several minutes to boot up a server or VM.
  - For each application, we had to install `OS` and `Application Dependencies` separately.
  - `Maintenance` of each server or VM was a challenge.
  - `Scaling` of application was a challenge.


- Docker Resolved above issues, but docker also has some drawbacks, which were benefits of traditional approach.
  - `Security` is a concern in docker. If one container is compromised, it can compromise other containers as well.
  - `Large number of containers` can be difficult to manage.
  - `Monitoring` of containers is a challenge.
  - `Environment specific` applications were not possible, as here we are using single host OS.


#### Some Basic Terminologies Related to Docker
- `Docker Engine:` Docker Engine is the core component of Docker, as it works on top of Host Machine, and manages the docker containers. 
  It is `responsible for starting, stopping, scaling of containers.`


- `Docker Image:` Docker Image is `lighweight`, `portable` and `read-only` template that contains all the required things needed to run an 
           application. It is `responsible for creating containers.` Docker Image is created using `Dockerfile`. Docker Image is 
           `immutable`, means we can not change it. Docker Images are stored on `Docker Registry`.


- `Docker Container:` Docker Container is a `runnable instance` of Docker Image. It is `responsible for running applications`. Docker 
        Container is created using Docker Image. Docker Container is `mutable`, means we can change it. Docker Container is stored on 
        `Docker Host`.


- `Docker Registry:` Docker Registry is a `repository` for Docker Images. Docker Registry is `responsible for storing Docker Images`. 
        Docker Registry can be `public` or `private`. Docker Registry can be `hosted` or `managed`.


- `Docker Compose:` It is a tool which is enables developers to `define and run multi-container docker appplications`. Docker compose uses 
        `YAML` file to configure the application services. Then, with a single command, we can create and start all the services from 
        our configuration.


- `Dockerfile:` Dockerfile is a simple `script` or `text-file` that contains all commands instructions in order to build a docker image. It
        defines the base image, application code, and the required dependencies. 


#### _**Some Basic Docker Commands**_
| Command                                                                         | Execution                                                                                                                   |
|:--------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------|
| `docker -v`                                                                     | to see the docker version.                                                                                                  |
| `docker version`                                                                | to see the complete docker information with version.                                                                        |
| `docker image ls OR docker images`                                              | List all images available on your local machine.                                                                            |
| `docker search [image-name]`                                                    | to search the images available in docker hub.                                                                               |
| `docker history [image-name OR image-id]`                                       | to see the history of docker image steps used to create the container.                                                      | 
| `docker image rm [image-id]`                                                    | to remove a image from docker hub.                                                                                          |                                      
| `docker pull [image-name]:[tag]`                                                | Download an image from docker registry, ex: Docker hub                                                                      |
| `docker build -t [image-name] [path]`                                           | Build an image from `Dockerfile` where <path> is directory containing Dockerfile.                                           |
|                                                                                 |                                                                                                                             |
| `docker run [image-name OR image-id]`                                           | to create the container.                                                                                                    |
| `docker ps -a`                                                                  | to see available containers (Running OR stopped).                                                                           |
| `docker rm [container-id OR container-name]`                                    | to remove the container.                                                                                                    |
| `docker rm -f [container-id OR container-name]`                                 | to remove the running container.                                                                                            |
| `docker [start OR stop] [container-id OR container-name]`                       | to start and stop the container.                                                                                            |
| `docker exec -it [container-id] /bin/bash`                                      | to Enter into already running container.                                                                                    |
| `docker attach [container-id]`                                                  | to attach with already running container.                                                                                   |
|                                                                                 |                                                                                                                             |
| `docker commit [container-id] [image-name]:[tag]`                               | to create image from modified container.                                                                                    |
| `docker image save [image-name]:[tag] -o [path]`                                | to save an image on the local machine as .tar.gz Ex: docker image save demo:latest -o C:/Users/Downloads/<file-name>.tar.gz |
| `docker image load -i [path]`                                                   | to load an image from local machine to docker.                                                                              |
|                                                                                 |                                                                                                                             |
| `docker image prune -a`                                                         | to remove the unused images from docker which doesn't have any container.                                                   |
| `docker container prune`                                                        | to remove the unused/Stopped containers from docker.                                                                        |
| `docker volume prune`                                                           | to remove the unused volume.                                                                                                |
| `docker network prune`                                                          | to remove the unused network.                                                                                               |
| `docker system prune -a`                                                        | to remove all unused objects such as images, containers, volumes.                                                           |
|                                                                                 |                                                                                                                             |
| `docker run -d -p [host_port]:[container_port] --name [container_name] [image]` | Run container from an image, maps host port to container port.                                                              |
| `docker container logs [container-id OR container-name]`                        | Show the logs of service running inside a container.                                                                        |
| `docker info`                                                                   | Displays system wise information regarding docker installation.                                                             |


#### Dockerfile Instructions
- Docker can build images automatically by reading the instructions from a `Dockerfile` which contains some text instructions.
- Some of the useful commands are `FROM`, `ADD`, `COPY`, `
- [Reference](https://docs.docker.com/engine/reference/builder/)


#### Manage Data in Docker
- Docker uses a `writable layer` to store all files created inside a container, but this `writable layer` is `removed` when the container is removed. 
  So, if we want to `persist` the data, we need to use `volumes mount` or `bind mounts`.
- These layer is tightly coupled with the host machine, so it's difficult to move data from a running container.
- These layer requires `storage driver` to manage file system, and this driver uses Union file system from Linux Kernel.
----------------------

- So, Docker has two options (mentioned above), through which data can be stored on host machine, and data is persisted. 
- So, to attach a volume or bind mount to a container, we need to use `docker run` command with `-v` or `--volume` option, and for tmpfs, use `--tmpfs`.
- Now, we can use `--mount` option instead of `-v` or `--volume` option, as it's more explicit and verbose.
- Check all the commands description `docker run --help`.
- Three Types of Mounts are there in docker:
1. `tempfs Mount`:
    - Temporary Storage file system.
    - Command: `docker container run -d -p 8080:80 --name=my-C1 --mount type=tmpfs,destination=/mylogs [image-name]`
    - It's a `temporary storage`, so it's `not persisted` on host machine.
2. `Bind Mount`:
   - It's a `directory` on the `host machine`, which is `mounted` on the `container`.
   - It is controlled by the host machine OS, not by the docker.
   - Command: `docker container run -d -p 8080:80 --name=my-C2 --mount type=bind,src={SOURCE_LOCATION_OF_DOCKER_HOST_MACHINE_TO_STORE_CONTAINER_DATA},dst={LOCATION_DOCKER_CONTAINER_WHERE_DATA_STORED} [image-name]`
3. `Volumes`:
   - It is controlled by Docker, not by Host machine OS.
   - Volumes are created under Location `{host_path}/docker/volume/{volume_name}`
   - Commands for Volume:
     - `docker volume create [volume-name]`
     - `docker volume [ls OR list]`
     - `docker volume rm [volume-name]`
   - Firstly create a volume using the above first command
   - Command: `docker container run -d -p 8080:80 --name=my-C3 --volume [volume-name]:[location directory for docker container logs] [image-name]`


#### How to Push Docker Image to Docker Hub
 + Create a Docker Hub Account. 
 + In the local, create a docker image using `docker build -t [docker-hub-username]/[image-name]:[tag] .` if not already exist.
 + If Image is already created, then tag it using `docker tag [image-name]:[tag] [docker-hub-username]/[image-name]:[tag]`.
 + Login to docker hub using `docker login`.
 + Push the image to docker hub using `docker push [docker-hub-username]/[image-name]:[tag]`.
 + Now, we can see the image on docker hub.d2                                                   


#### Docker Networking
- Docker networking exists so that containers can communicate with each other, with hosting system and with the outside world.
- docker provides five standard types of networks:
  - `Bridge Network`: **It's a default network**, and it's a private internal network created by docker on the host machine. 
                      It's a single host network, means containers on different hosts can not communicate with each other.
  - `Host Network`: It's a multi host network, means containers on different hosts can not communicate with each other.
  - `Overlay Network`: It's a multi-host network, means containers on different hosts can communicate with each other.
  - `Macvlan Network`: It's a multi-host network, means containers on different hosts can communicate with each other.
  - `None Network`: It's a single host network, means containers on different hosts can not communicate with each other.
- **Some Docker networking commands**

| Command                                           | Execution                                                                                       |
|:--------------------------------------------------|:------------------------------------------------------------------------------------------------|
| `docker network [COMMAND]`                        | `connect`: to connect a network to a running container.                                         |
|                                                   | `create`: to create a network.                                                                  |
|                                                   | `disconnect`: to disconnect a container from a network.                                         |
|                                                   | `inspect`: display detailed info of network.                                                    |
|                                                   | `ls`: List of all the networks present in docker.                                               |
|                                                   | `prune`: Remove all unused networks.                                                            |
|                                                   | `rm`: Remove >= 1 networks.                                                                     |
| `docker network create [OPTIONS] [NETWORK-NAME]`  | help to create a network with any network-name.                                                 |
| `docker network inspect [OPTIONS] [NETWORK-NAME]` | help to inspect a given network, will get a json which contains information of created network. |
| `docker network rm [NETWORK-NAME OR NETWORK-Id]`  | help to remove an existing network.                                                             |
| `docker network prune`                            | All un-used network will be removed.                                                            |
**Steps to communicate between two containers (On bridge network)**
1. Create a container using an image named [container-1].
2. Create a container using an image named [container-2].
3. Create a network named [network-1] with bridge, using `docker network create network-1 -d bridge` (if do not specify bridge, default is also bridge network).
4. Connect both the containers to the network [network-1] using `docker network connect network-1 [container-1]` and `docker network connect network-1 [container-2]`.
5. Now, check if both the containers are able to communicating.
    1. for this, run `docker exec -it container-2 ping container-1`. If it's able to ping, then it's communicating.

**Default Bridge Network v/s Custom Bridge Network**
- In default bridge network, it is not allowed to ping the container using container name, but in custom bridge network, it is allowed.
- Try to connect two containers with default bridge network, and try to ping one container from another using container name, it will not work.
- Try to connect two containers with custom bridge network, and try to ping one container from another using container name, it will work.

**macvlan Network**
- When multiple containers are connected to the macvlan network, each container will get a unique MAC address, and it will be able to communicate with each other.
- But, it will not be able to communicate with the host machine, and vice-versa.
**Ipvlan Network**
- When multiple containers are connected to the Ipvlan Network, each container will get a unique IP address, and it will be able to communicate with each other.
** Check for both the networks by creating two containers, connect with each type of network, and do network inspect for both network.
```
docker network create ipnetwork -d ipvlan
docker network create macnetwork -d macvlan

# check for ipnetwork
docker run -itd --name=container-1 --network=ipnetwork alpine
docker run -itd --name=container-2 --network=ipnetwork alpine
docker network inspect ipnetwork
[{
    "Name": "ipnetwork",
    "Id": "5a16fd8c8c856e4b4eb2ec6e72fa5c854f52f544150451789770a79a16bee292",
    "Created": "2024-01-25T18:49:09.335961036Z",
    "Scope": "local",
    "Driver": "ipvlan",
    "EnableIPv6": false,
    "IPAM": {
        "Driver": "default",
        "Options": {},
        "Config": [
            {
                "Subnet": "172.20.0.0/16",
                "Gateway": "172.20.0.1"
            }
        ]
    },
    "Internal": false,
    "Attachable": false,
    "Ingress": false,
    "ConfigFrom": {
        "Network": ""
    },
    "ConfigOnly": false,
    "Containers": {
        "3a4310788ebf2e5e44623f55e83a8e505319417898602a884802b4714f5d1162": {
            "Name": "intelligent_taussig",
            "EndpointID": "9d167182ad73c8d3115a5e12fd44aad34b6458addcb3a78de16d6aacee005aee",
            "MacAddress": "",
            "IPv4Address": "172.20.0.3/16",
            "IPv6Address": ""
        },
        "74409b2e07d18612c79354daaa461677a982754554273ad2ea85023e09b2b165": {
            "Name": "my-C3",
            "EndpointID": "2ac80ff075a4523deaaa503a357b306dfe10d04e413f59834666a69cb59b157a",
            "MacAddress": "",
            "IPv4Address": "172.20.0.2/16",
            "IPv6Address": ""
        }
    },
    "Options": {},
    "Labels": {}
}]


# check for macnetwork
docker run -itd --name=container-1 --network=macnetwork alpine
docker run -itd --name=container-2 --network=macnetwork alpine
docker network inspect macnetwork 
[{
    "Name": "macnetwork",
    "Id": "441d2649e1bbd8abf2c6a7d62777a4aaf5078064205f217a1ac17e1f79e7daa5",
    "Created": "2024-01-25T18:48:50.371095897Z",
    "Scope": "local",
    "Driver": "macvlan",
    "EnableIPv6": false,
    "IPAM": {
        "Driver": "default",
        "Options": {},
        "Config": [
            {
                "Subnet": "172.19.0.0/16",
                "Gateway": "172.19.0.1"
            }
        ]
    },
    "Internal": false,
    "Attachable": false,
    "Ingress": false,
    "ConfigFrom": {
        "Network": ""
    },
    "ConfigOnly": false,
    "Containers": {
        "3a4310788ebf2e5e44623f55e83a8e505319417898602a884802b4714f5d1162": {
            "Name": "intelligent_taussig",
            "EndpointID": "32db499f0ff1ce8f2efbcda49b337265ee79dedb16ed1fce838720009ec2de53",
            "MacAddress": "02:42:ac:13:00:03",
            "IPv4Address": "172.19.0.3/16",
            "IPv6Address": ""
        },
        "74409b2e07d18612c79354daaa461677a982754554273ad2ea85023e09b2b165": {
            "Name": "my-C3",
            "EndpointID": "9b099f300e1fc939c2bc0dbca7284d7d53890f594a6eb7a8828e16f85b134c75",
            "MacAddress": "02:42:ac:13:00:02",
            "IPv4Address": "172.19.0.2/16",
            "IPv6Address": ""
        }
    },
    "Options": {},
    "Labels": {}
}]
```

**None network**
- When a container is connected to the None network, it will not be able to communicate with any other container, and with the host machine as well.

**How to work with Overlay network**
- Overlay network is a multi host network, which means containers running on multiple hosts can communicate with each other.
- For testing this overlay network, we are going to create EC2 instances as follows:
  - Master Node
  - Worker Node 1
  - Worker Node 2

- On AWS, create two EC2 instances with Ubuntu 20.04, and install docker on both the instances.
- connect with those instances using ssh command `ssh -i key.pem ubuntu@public-ip`.
- Change the hostname using `sudo hostnamectl set-hostname <hostname>`.
- Installation Steps for Docker on each EC2 container:
  - `sudo apt-get update`
  - `sudo apt install docker.io -y`
  - `sudo usermod -aG docker ${USER}`
  - `docker version`

