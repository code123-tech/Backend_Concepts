Contents
- [What is Docker](#_what-is-docker_)
- [Some Basic Terminologies Related to Docker](#some-basic-terminologies-related-to-docker)
- [Some Basic Docker Commands](#_some-basic-docker-commands_)
- [Dockerfile Instructions](#dockerfile-instructions)
- [Manage Data in Docker](#manage-data-in-docker)

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


#### Dockerfile Instructions
- Docker can build images automatically by reading the instructions from a `Dockerfile` which contains some text instructions.


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