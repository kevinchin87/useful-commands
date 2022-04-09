# Commands for Docker

## Dockerfile for Express

```
FROM node:16.14.0-alpine //define docker's os image
WORKDIR /app //define work directory in the docker
COPY package.json . //npm package will be cache, and improve the docker compile time if no update on npm library
RUN npm install
COPY . ./ //copy the working directory to the docker
ENV PORT 3004 //define variable
EXPOSE $PORT //whitelist port
CMD ["npm", "run", "start"] //start code
```
## .dockerignore for Express

```
node_modules
Dockerfile
.dockerignore
.git
.gitignore
```

## Build docker image

```
docker build -t [tag-name] [file-path]
docker build -t node-app-image .
```

|Option|Description|
|:-:|:-|
|-t|Name and optionally a tag in the 'name:tag' format|

## Run docker image

```
docker run -p [local-port]:[container-port] -d --name [container-name] [tag-name]
docker run -p 3001:3000 -d --name node-app node-app-image
```

|Option|Description|
|:-:|:-|
|-d|detech mode, run container in background and print container ID|
|-p|define local and container port mapping
|--name|container name|

## Run docker image with bind volume

This is for development purpose, where we use nodemon in container. Bind volume allow us to update the code in container when the source code is changed. 

```
docker run -v [local-file-path]:[container-file-path] -p [local-port]:[container-port] -d --name [container-name] [tag-name]
docker run -v C:\Users\kevin\Documents\Programming\tro\tro_discord_msg\:/app -p 3001:3000 -d --name node-app node-app-image
```

We can use shortcut to point current directory
```
docker run -v /$(pwd):/app -p 3001:3000 -d --name node-app node-app-image
```

|Shortcut|Description|
|:-:|:-|
|%cd%|Window Shell|
|${pwd}|Power Shell|
|$(pwd)|Linux or Mac|
|/$(pwd)|Git Bash|

Bind anonymous volume to ensure deleting local node_module will not delete the node_module folder in container

```
docker run -v /$(pwd):/app -v //app//node_modules -p 3001:3000 -d --name node-app node-app-image
```

use // for Git Bash, / for the rest? test it around.

Ensure bind volume in container is read only, meaning new generated files in container will not sync to local machine

```
-v /$(pwd):/app:ro
```

|Option|Description|
|:-:|:-|
|ro|Read Only|

## Access docker container

```
docker exec -it [container-name] sh|bash
docker exec -it node-app sh
```

|Option|Description|
|:-:|:-|
|-i|Keep STDIN open even if not attached|
|-t|Allocate a pseudo-TTY|

## Delete docker container

```
docker rm [container-name] -f
docker rm node-app -f
```

|Option|Description|
|:-:|:-|
|-f|Force the removal of a running container (uses SIGKILL)|

## List docker image

```
docker image ls
```

## List all running docker container

```
docker ps
```

## List all docker container

```
docker ps -a
```

## Get container logs

```
docker logs [container-name]
docker logs node-app
```
