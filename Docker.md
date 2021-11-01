
# DOCKER

## Container
Container is simply another process on your machine that has been isolated from all other processes on the host machine.
That isolation leverages kernel namespaces and cgroups. You can start a container based on the images you build.
Running a container launches your application with private resources, securely isolated from the rest of your machine.

## Container Image
When running a container, it uses an isolated filesystem. This custom filesystem is provided by a container image.
Since the image contains the container's filesystem, it must contain everything needed to run an application - all dependencies,
configuration, scripts, binaries, environment variables, a default command to run, and other metadata.
Docker image is a private file system just for your container and it provides all the files and code your container needs.

## Sharing
You can save and share your image on Docker Hub to enable other users to easily download and run the image on any destination machine.

## Dockerfile
Docker can build images automatically by reading the instructions from a Dockerfile.
A Dockerfile is a text document that contains the instructions to assemble a Docker image.
When we tell Docker to build our image by executing the `docker build` command,
Docker reads these instructions, executes them, and creates a Docker image as a result.

Example of Dockerfile:
```
FROM node:12.18.1
ENV NODE_ENV=production

WORKDIR /app

COPY ["package.json", "package-lock.json*", "./"]

RUN npm install --production

COPY . .

CMD [ "node", "server.js" ]
```

The docker build command builds an image from a Dockerfile and a context: `docker build .`  
`.` - tells to use the current directory as build context.

[Best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)

[Build your NodeJS Image](https://docs.docker.com/language/nodejs/build-images/)
