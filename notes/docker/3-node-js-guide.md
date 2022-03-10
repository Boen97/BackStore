## Build your Node Image

### Enable BuildKit

> BuildKit allows you to build Docker images efficiently.
- BuildKit is enabled by default for all user on Docker Desktop.

- if you are running Docker in Linux, you can enable BuildKit by using an environment variable;
  `$ DOCKER_BUILDKIT=1 docker build .`

- to enable docker BuildKit by default, set daemon configuration in `/etc/docker/daemon.json`
- and restart the daemon.
  ```json
  {
      "features": {"buildkit": true}
  }
  ```

### Create a Dockerfile for Node.js

- `docker-build -f <specify a dockerfile>`
  - `-f` specific a dockerfile
  - recommend using the default name `Dockerfile`

- `# syntax` parser directive
  - `# syntax=docker/dockerfile:1`
  - this directive instructs the Docker builder what syntax to use when parsing the Dockerfile
  - allows older Docker versions with BuildKit enabled to upgrade the parser before starting the build
  - recommend `docker/dockerfile:1`, which always points to the latest release of the version 1 syntax.
  - BuildKit automatically checks for updates of the syntax before building, making sure you are using the most current version.
 
- `FROM node:12.18.1`

- `ENV NODE_ENV=production`
  - specify the environment in which an application is running

- `WORKDIR /app`
  - this instructs the Docker to use this path as the default location of all subsequnce command.

- `COPY ["<src1>", "<src2>", ..., "<dest>"]`

- `RUN npm install --production`

- `CMD ["node", "server.js"]`
  - tell Docker what command we want to run when our image is run inside of a container.
  
### Build Image

- `docker build` command builds Docker images from a Dockerfile and a "context".
- The Docker build process can access any of the files located in the context.
- `--tag` used to set the name of the image and an optional tag in the format `name:tag`.
- if you do not use a tag, docker will use 'latest' as its default tag.
- `docker build --tag node-docker .`

### view local images.
- `docker images`

### Tag images.

- an image name is made up of slash-seperated name components.
- name components may contain lowercase letters, digits, and separators.
- a separator is defined as a period, one or two underscores, or one or more dashes.
- a name component may not start or end with a separator.
- an image is made up a manifest and a list of layers.
- a tag points to a combination of thest artifacts.
- you can have multiple tags for an image.

- `docker tag node-docker:latest node-docker:v1.0.0`
- thest two images have the same image id, different image tag.

- remove tag
  `docker rmi node-docker:v1.0.0`
