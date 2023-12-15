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


#### _**Some Basic Commands**_

| Command                                                                         | Execution                                                                         |
|:--------------------------------------------------------------------------------|:----------------------------------------------------------------------------------|
| `docker -v`                                                                     | to see the docker version.                                                        |
| `docker version`                                                                | to see the complete docker information with version.                              |
| `docker image ls OR docker images`                                              | List all images available on your local machine.                                  |
| `docker search [image-name]`                                                    | to search the images available in docker hub.                                     |
| `docker history [image-name OR image-id]`                                       | to see the history of docker image steps used to create the container.            | 
| `docker image rm [image-id]`                                                    | to remove a image from docker hub.                                                |                                      
| `docker pull [image-name]:[tag]`                                                | Download an image from docker registry, ex: Docker hub                            |
| `docker build -t [image-name] [path]`                                           | Build an image from `Dockerfile` where <path> is directory containing Dockerfile. |
|                                                                                 |                                                                                   |
| `docker run [image-name OR image-id]`                                           | to create the container.                                                          |
| `docker ps -a`                                                                  | to see available containers (Running OR stopped).                                 |
| `docker rm [container-id OR container-name]`                                    | to remove the container.                                                          |
| `docker rm -f [container-id OR container-name]`                                 | to remove the running container.                                                  |
| `docker [start OR stop] [container-id OR container-name]`                       | to start and stop the container.                                                  |
| `docker exec -it [container-id] /bin/bash`                                      | to Enter into already running container.                                          |
| `docker attach [container-id]`                                                  | to attach with already running container.                                         |
|                                                                                 |                                                                                   |
| `docker run -d -p [host_port]:[container_port] --name [container_name] [image]` | Run container from an image, maps host port to container port.                    |
