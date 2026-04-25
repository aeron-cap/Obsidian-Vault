- Provides the ability to package and run application in a loosely isolated environment called a container.
- the isolation and security allows us to run many containers simultaneously on a given host.
- **Containers**
	- lightweight and contain everything needed to run the application so we don't need to rely on what's installed on the local host.
##### [**GENERAL COMMANDS**](https://docs.docker.com/get-started/docker_cheatsheet.pdf)
*Start the docker daemon*
- `docker -d`
- `sudo systemctl start docker`
*Get help with Docker*
- `docker --help`
*Display system-wide info*
- `docker info`
##### **IMAGES**
- Docker images are lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.
*Build an image from a Dockerfile*
- `docker build -t <image-name>`
*List local images*
- `docker images`
*Delete an Image*
- `docker rmi <image_name>`
*Remove all unused images*
- `docker image prune`
##### **CONTAINERS**
- A runtime instance of a docker image. A container will always run the same, regardless of the infrastructure. Containers isolate software from its environment and ensure that it works uniformly despite differences for instance between development and staging.
*Start or stop an existing container*
- `docker start|stop <container_name>`
*Open a shell inside a running container*
- `docker exec -it <container_name> sh`
*List all docker containers (running and stopped)*
- `docker ps --all`
*List all running containers*
- `docker ps`
*View resource usage stats*
- `docker container stats`
##### **COMPOSE**
- Tool for defining and running multi-container applications. It is the key to unlocking a streamlines and efficient development and deployment experience.
