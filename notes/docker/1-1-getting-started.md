> `docker run -d -p 80:80 docker/getting-started`
- `-d` run the container in detached mode (in the background)
- `-p 80:80` map port 80 of the host to port 80 in the container
- `docker/getting-started` the image to use

- you can combine single character flags to shorten the full command.
  `docker run -dp 80:80 docker/getting-started`
   
### What is a container?
> a container is a sandboxed process on your machine that is isolated from all other processes on the host machine.
> That isolation leverages `kernel namespace and cgroups`, features that have been in Linux for a long time.
- Docker has worked to make these capabilites approachable and easy to use.
1. is an runnable instance of an image. you can create, start, stop, move, or delete a container using the DockerAPI or CLI.
2. can be run on local machines, virtual machines or deployed to the cloud.
3. is portable can be run on any OS
4. Containers are isolated from each other and run their own software, binaries, and configurations.

### What is a container image?
- when running container, it uses a isolated filesystem.
- This custom filesystem is provided by a **container image**
- Since the image contains the container's filesystem, it must contain everything needed to run an application
  - all dependencies, configuration, scripts, binaries, etc.
- The image also contains other configuration for the container, such as environment variables, a default command to run, and other metadata.

> you can think of a container as an extended version of `chroot`. The filesystem is simple comming from the image.
> But, a container adds additional isolation not avaliable when simply using  chroot.

### build the app's container image
- in order to build the application, we need to use a `Dockerfile`
- A `Dockerfile` is simple a text-based script of instructions that is used to create a container image.
- the `Dockerfile` content
```Dockerfile
# syntax=docker/dockerfile:1
FROM node:12-alpine
RUN apk add --no-cache python2 g++ make
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
EXPOSE 3000
```
    - start from the `node:12-alpine` image
    - use `yarn` to install our application's dependencies
    - The `CMD` directive specifies the default command to run when starting a container from this image.
- build the container image
  ```docker build -t getting-started .```
  - `-t` flag tags our image. think of this simply as a human-readable name for the final image.
  - `.` tells the Docker should look for `Dockerfile` in the current directory.

### start an app container
`docker run -dp 3000:3000 getting-started`
- `-d` running the new container in detached mode (in the background)
- `-p` creating a mapping between the host's port 3000 to the container's port 3000.
  - without the port mapping, we wouldn't be able to access the application.

### replace the old container
- ro remove a container, it first needs to be stopped.
#### remove a container using the CLI
1. get the ID of the container using the `docker ps` command
   `docker ps`
   
2. use the `docker stop` command to stop the container.
   `docker stop <the-container-id>`

3. once the container is stopped, you can remove the container using `docker rm` command
   `docker rm <the-container-id>`
   
4. or you can stop and remove a container in a single command by adding the 'force' flag to the `docker rm` command.
   `docker rm -f <the-container-id>`

### update the source code.

- when you finished edit your code, you need to stop or remove the old container, and rebuild the image, then start the new container.
1. `docker rm -f <the-container-id>`
2. `docker build -t getting-started .`
3. `docker run -dp 3000:3000 getting-started`

### Share the application.
- to share Docker images, you have to use a Docker registry.
- the default registry is Docker Hub.

#### Create a repo
1. Sign in Docker Hub
2. create a repository

#### Push the image to the repository
1. `docker image ls`
2. `docker login -u rhymechiang`
3. `docker tag getting-started rhymechiang/getting-started`
4. `docker push rhymechiang/getting-started`
