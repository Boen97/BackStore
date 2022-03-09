## Use Docker Compose

> Docker Compose is tool that was developed to help define and share multi-container applications.

> The big advantage of using Compose is you can define your application stack in a file, keep it at the root of your project repo.

- `docker-compose version`

### Create the Compose file

- at the root of the project, create a file named `docker-compose.yml`

### Define the app service

1. first, define the service entry and the image for the container.
   we can pick any name for the service.
   The name will automatically become a network alias
```shell
docker run -dp 3000:3000 \
-w /app -v "$(pwd):/app" \
--network todo-app \
-e MYSQL_HOST=mysql \
-e MYSQL_USER=root \
-e MYSQL_PASSWORD=secret \
-e MYSQL_DB=todos \
node:12-alpine \
sh -c "yarn install && yarn run dev"
```

```yaml

version: "3.7"

services:
    app:
        image: node:12-alpine
        command: sh -c "yarn install && yarn run dev"
        ports:
            - 3000:3000
        working_dir: /app
        volumes:
            - ./:/app
        environment:
            MYSQL_HOST: mysql
            MYSQL_USER: root
            MYSQL_PASSWORD: secret
            MYSQL_DB: todos
    mysql:
        imgae: mysql:5.7
        volumes:
            - todo-mysql-data:/var/lib/mysql
        environment:
            MYSQL_ROOT_PASSWORD: secret
            MYSQL_DATABASE: todos

volumes:
    todo-mysql-data:

```

### run the application stack

- `docker-compose up -d`
  - `-d` run everything in the background

- `docker-compose logs -f`

- `docker-compose logs -f app`

> Waiting for the DB before starting the app
> Docker doesn't have any built-in support to wait for another container to be fully up.
> it's the frameworks's job to manage the starting order.

### tear it all down
- `docker-compose down`
> by default, named-volumes in your compose file are not removed when down.
> if you want to remove volumes, you need to add `--volumes` flag.
