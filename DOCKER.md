# Documentation for Docker
## Docker Image
- The docker image is blue blueprint of some already-made containers.
- Consider docker images as a drawing of a picture of your fav. toy. It contains the details of how your toy looks.
Consider it like a magical box holding your favorite toy inside. You can use the magical box to create an exact copy of your toy when you have your image.
- Actual Definition: It is a snapshot or a blueprint of the complete environment of an application. It includes everything like what the application needs to run, such as libraries, dependencies, config, etc. It kind of encapsulates the application and all the requirements together.

## Container
- A container is an actual instance of the environment configured by the image. When we run a docker image, it creates a live and running container. These containers are isolated and lightweight virtual machines.
- A big difference between containers and VMs is that containers share the host OS kernel.

## Commands
- To install image.
```
docker pull image_name(alpine:3.18.2)
```
- To remove image
```
docker rmi image_name
```
- To run docker image.
```
docker run -it image_name(alpine:3.18.2)
-it flag is for interact with container directly
docker run -it alpine:3.18.2 ls
--rm flag is when you execute the command, it imediately detete the running container.
docker run -it --rm image_name
```
- To list all the containers.
```
docker ps
```
- To run container in background ( it will give you a hash code), go inside the container and then run given command.
```
docker run --detach -it image_name
```
- To go inside the container of background running container.
```
docker attack container_hashcode
```
- To delete the container.
```
docker rm container_name
```
- To directly remove background container.
```
docker kill container_name
docker rm container_name
```
- To give custom name to background container.
```
docker run -it --detach --name custom_node(custom name of container name) image_name(node).
```
- To run docker image in background with singal flag rather than -it and detach.
```
docker run -dit image_name
```
- docker run -it image_name bash to go insider linux directly inside the container.
- `docker inspect image_name` to get details about the image.
- To pause the container.
```
doker pause container_id
```
- To unpause the container.
```
docker unpause container_id
```
- docker run create a new container but if u don't want to create a new container then use "exec" command in place of run.
```
docker exec -it container_name/id
```
## Own docker image( Docker file)
- file name 'Dockerfile"
- FROM image_name (this will be base container for your container).
- CMD []:- ex.["node","-e","console.lo(100)"], You can't have multiple CMD or it will excecute last one. 
- TO build a new docker container
```
docker build .
```
- Now run the image by run command. 
- Whole code at once.
```

FROM node
CMD ["node","-e","console.lo(100)"]

```
- To give name to docker image during building
```
docker build -t your_image_name .
```
## To create docker file insider project
- WORKDIR or working directory, if you have not this directory then it create this directory.
- To copy everyfile insider working directory.
```
COPY source_directory destination_directory(or WORKDIR)
```
- TO run specific command use "RUN".
- Final code.
```
FROM node

WORKDIR /developer/nodejs/my-server

COPY . .

RUN npm ci

CMD ["node","index.js"]

```
- So basic docker file is ready.

- Here is the problem, you can't do ctl c to exit and also when you referece the page, then it don't work. Because container is in isolated environment unless you mentioned how host and container should communicate it will not.
- `--init` flag to control the process insider container from host machine. This will solve the ctl c error problem.
- You have to expose the container to port. so use '--publish host_port:container_port' to communicate. 
```
docker run -it --init --publish 3001:3000 container_name
```
## Doker file when have to copy file from github and ENV setup
- TO copy file from github repo.
```
FROM node

WORKDIR /developer/nodejs/app_from_github

RUN apt-get update && apt-get install -y git

RUN git clone repo_link .

RUN npm ci

CMD ["npm", "start"]

```
- TO config ENV file, use ENV command and write what you need eg.
```
ENV PORT=3000
```
## TO delete cache file or everything (all images and containers)
```
docker system prune -a
```

