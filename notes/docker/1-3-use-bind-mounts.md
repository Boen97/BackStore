## Use bind mounts

> names volumes are great if we simply want to store data, since we don't have to warry about where the data is stored.

> with `bind mounts`, we control the exact mountpoint on the host.
> we can use this to persist data, but it's often used to provide additional data into containers.
> when working on an application, we can use a bind mount to mount our source code into the container
> to let it see code changes, respond, and let us see the changes right away

- for Node-based applications, `nodemon` is a great tool to watch for file changes and then restart the application.
- There are equivalent tools in most other languages and frameworks.

### Start a dev-mode container

- To run our container to support a development workflow, we will do the following:
1. mount our source code into the container
2. Install all dependencies, including the dev dependencies
3. start nodemon to watch for filesystem changes.

```shell
docker run -dp 3000:3000 \
-w /app -v "$(pwd):/app" \
node:12-alpine \
sh -c "yarn install && yarn run dev"
```
- `-w /app` 
  - sets the working directory or the current directory that the command will run from.

- `-v "$(pwd):/app"`
  - bind mount the current directory from the host in the container into the /app directory

- `node:12-alpine`
  - the image to use.

- `sh -c "yarn install && yarn run dev"`
  - starting a shell using sh command and running yarn install to install all dependencies.

> watch logs
`docker logs -f <container-id>`
- when done wathcing logs, exit out by hitting Ctrl-C


