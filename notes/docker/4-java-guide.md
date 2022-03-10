- `CMD ["./mvnw", "spring-boot:run"]`
  - tell Docker what command we want to run when our image is executed inside a container.

```
$ curl --request GET \
--url http://localhost:8080/actuator/health \
--header 'content-type: application/json'
```

- `docker run --publish 8080:8080 java-docker`
  - `--publish` flag (`-p` for short)

### stop, start, and name containers.
- Docker generate a randon name for the container if we didn't provide the name when container starting

- `docker ps --all`
- `docker ps -a`
  - list all containers in the machine, including the stopped containers.
- `docker restart <container-name | container-id>`

- to name a container
  `docker run --rm -dp 8080:8080 --name springboot-server java-docker`
  - `--rm` automatically delete the container when it exits
  - `--name` name the container.

### use containers for development.
`docker volume create mysql-data`
`docker volume create mysql-config`
`docker network create mysqlnet`
```
docker run -it --rm -d -v mysql_data:/var/lib/mysql \
-v mysql_config:/etc/mysql/conf.d \
--network mysqlnet \
--name mysqlserver \
-e MYSQL_USER=petclinic -e MYSQL_PASSWORD=petclinic \
-e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=petclinic \
-p 3306:3306 mysql:8.0.23
```

`CMD ["./mvnw", "spring-boot:run", "-Dspring-boot.run.profiles=mysql"]`

`docker build --tag java-docker .`

```
docker run --rm -d \
--name spring-boot-server \
--network mysqlnet \
-e MYSQL_URL=jdbc:mysql//mysqlserver/petclinic \
-p 8080:8080 java-docker
```

### Use Compose to develop locally

- create `docker-compose.dev.yml` file

```yaml
services:
  petclinic:
    build:
      context: .
    ports:
      - 8000:8000
      - 8080:8080
    environment:
      - SERVER_PORT=8080
      - MYSQL_URL=jdbc:mysql://mysqlserver/petclinic
    volumes:
      - ./:/app
    command: ./mvnw spring-boot:run -Dspring-boot.run.profiles=mysql -Dspring-boot.run.jvmArguments="-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:8000"

  mysqlserver:
    image: mysql:8.0.23
    ports:
      - 3306:3306
    environment:
      - MYSQL_ROOT_PASSWORD=
      - MYSQL_ALLOW_EMPTY_PASSWORD=true
      - MYSQL_USER=petclinic
      - MYSQL_PASSWORD=petclinic
      - MYSQL_DATABASE=petclinic
    volumes:
      - mysql_data:/var/lib/mysql
      - mysql_config:/etc/mysql/conf.d

volumes:
  mysql_data:
  mysql_config:
```

- `docker-
compose -f docker-compose.dev.yml up --build`
  `--build` Docker will compile our image and then starts the containers.

### run your tests.

`docker run -it --rm --name springboot-test java-docker ./mvnw test`

#### Multi-stage Dockerfile for testing

```Dockerfile
# syntax=docker/dockerfile:1

FROM openjdk:16-alpine3.13 as base

WORKDIR /app

COPY .mvn/ .mvn
COPY mvnw pom.xml ./
RUN ./mvnw dependency:go-offline
COPY src ./src

FROM base as test
CMD ["./mvnw", "test"]

FROM base as development
CMD ["./mvnw", "spring-boot:run", "-Dspring-boot.run.profiles=mysql", "-Dspring-boot.run.jvmArguments='-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:8000'"]

FROM base as build
RUN ./mvnw package

FROM openjdk:11-jre-slim as production
EXPOSE 8080

COPY --from=build /app/target/spring-petclinic-*.jar /spring-petclinic.jar

CMD ["java", "-Djava.security.egd=file:/dev/./urandom", "-jar", "/spring-petclinic.jar"]
```

- `docker build -t java-docker --target test .`
- `docker run -it --rm --name springboot-test java-docker`
> The CMD statement is not executed during the building of the image, but is executed when you run the image in a container

```Dockerfile

FROM base as test
RUN ["./mvnw", "test"] # The test will run during the image building

```

### RUN VS CMD VS ENTRYPONT
- RUN
  - RUN is an image build step, the state of the container after a RUN command will be committed to the container image.
  - A Dockerfile can have many RUN steps that layer on top of one another to build the image.

- CMD
  - CMD is the command the container executes by default when you launch the built image.
  - A Dockerfile will only use the final CMD defined.
  - The CMD can be overridden when starting a container with docker run $image $other_command.

- ENTRYPONT
  - ENTRYPOINT is also closely related to CMD and can modify the way a container starts an image.

### Multi-stage Dockerfile for development

- in the Dockerfile we have development stage
```Dockerfile
FROM base as development
CMD ["./mvnw", "spring-boot:run", "-Dspring-boot.run.profiles=mysql", "-Dspring-boot.run.jvmArguments='-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:8000'"]
```

- update `docker-compose.dev.yml` specific the development target.

```yaml
services:
 petclinic:
   build:
     context: .
     target: development
   ports:
     - 8000:8000
     - 8080:8080
   environment:
     - SERVER_PORT=8080
     - MYSQL_URL=jdbc:mysql://mysqlserver/petclinic
   volumes:
     - ./:/app
```

