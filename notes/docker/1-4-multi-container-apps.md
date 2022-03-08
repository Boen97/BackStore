## Multi container apps

> In general, each container should do one thing and do it well.
1. running multiple process will require a process manager (the container only starts one process).
   which add complexity to container startup/shutdown.
2. you don't want to ship your database engine with your app then.
3. separate container lets you version and update versions in isolation.

### Container Networking
> if two containers are on the same network, they can talk to each other, if they aren't, they can't.

> two ways to put a container on a network
1. Assign it at start.
2. connect an existing container.

- `docker network create todo-app`
  - create the network

- assign network when start mysql container
```shell
docker run -d \
--network todo-app --network-alias mysql \
-v todo-app-data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=secret \
-e MYSQL_DATABASE=todos \
mysql:5.7
```
- `--network-alias` mysql container are signed to "mysql" hostname, which can be find by other nodes in the network by DNS service.

- Docker will automatically create the volume for us.

- confirm the mysql container database are up and running
  `docker exec -it <mysql-container-id> mysql -u root -p`

### Connect to MYSQL

> make use of `nicolaka/netshoot` container, which ships a lot of tools that are useful for troubleshooting or debugging network issues.

- `docker run -it --network todo-app nicolaka/netshoot`
- `dig mysql`
  - `dig` is a useful DNS tool.
  

### running your app with MySQL
```shell
# for MySQL versions 8.0 and higher, make sure to include the following commands in mysql.
mysql> ALTER USER 'root' IDENTIFIED WITH mysql_native_password BY 'secret';
mysql> flush privileges;
```
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

- `MYSQL_HOST` the hostname for the running MYSQL server.

- `docker exec -it <mysql-container-id> mysql -p todos`
