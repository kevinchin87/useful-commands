# Commands for Docker

## Dockerfile for Express

```
FROM node:16.14.0-alpine //define docker's os image
WORKDIR /app //define work directory in the docker
COPY package.json . //npm package will be cache, and improve the docker compile time if no update on npm library
RUN npm install
COPY . ./ //copy the working directory to the docker
EXPOSE 3004 //whitelist port
CMD ["npm", "run", "start"] //start code
```
## .dockerignore

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

