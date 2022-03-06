## Docker overview

> Docker is an open platform for developing, shipping, and running applications.
> Docker enables you to separate your applications from your infrastructure so you can deliver software quickly.
> with Docker, you can manage your infrastructure in the same ways you manage your applications.

- by taking the advantage of Docker's methodologies for shipping, testing, and deploying code quickly
- reduce the delay between writing code and running it in production.

### The Docker platform

- container
  - Docker provides the ability to package and run an application in a loosely isolated environment called a container.
  
- The isolation and security allows you to run many containers simultaneously on a given host.

- containers are lightweight and contain everything needed to run the application
- so you do not need to rely on what is currently installed on the host.
- you can easily share containers while you work, and be sure that everyone you share with gets the same container that works the same way.

- Docker provides tooling and platform to manage the lifecycle of your containers:
1. Develop your application and its supporting components using containers.
2. The container becomes the unit for distributing and testing your application.
3. When you're ready, deploy your application into your production environment, as a container or an orchestrated service.
4. This works the same whether your production environment is a local data center, a cloud provider, or a bybrid of the two.

### What can I use Docker for?

> Fast, consistent delivery of your application.

- Docker streamlines the development lifecycle
  1. allow developers to work in standardized environments using local containers which provide your applications and services.
  2. Containers are great for continuous integration and continuous delivery (CI/CD) workflows.

- Consider the following example scenario:
1. your developers write code locally and share their work with their colleagues using Docker containers.
2. They use Docker to push their applications into a test environment and execute automated and manual tests.
3. when developers find bugs, they can fix them in the development environment, and redeploy them to the test environment for testing and validation.
4. when testing is complete, getting the fix to the customer is as simple as pushing the updated image to the production environment.
  
- Responsive deployment and scaling
1. Docker's container-based platform allows for highly portable workloads.
   - Docker containers can run on a developer's local laptop, on physical or virtual machines in a data center, on cloud or in a mixture of environments.
   
2. Docker's portability and lightweight nature also make it easy to dynamically manage workloads.
   - scaling up or tearing down applications and services as business needs dictate, in near real time.

- Running more workloads on the same hardware.
1. it provides a viable, cose-effective alternative to hypervisor-based virtual machines
   - so you can use more of your compute capacity to achieve your business goals.
2. Docker is perfect for high density environments and for small and medium deployments where your need to do more with fewer resouces.

### Docker architecture
- client-server architecture
- The Docker client talks to the Docker daemon
- Docker daemon
  - do the heavy lifting of building, running and distributing your Docker containers.
- The Docker client and daemon can run on the same system, or you can connect a Docker client to a remote Docker daemon.
- The Docker client and daemon communicat using a REST API
- Docker Compose
  - another Docker client that lets you work with applications consisting of a set of containers.

#### The Docker daemon
- The Docker daemon (dockerd) listens for Docker API requests and manage Docker objects such as images, containers, networks and volumns.
- A daemon can also communicat with other daemons to manage Docker services.

#### The Docker client
- The Docker client (docker) is the primary way that many Docker users interact with Docker.
- When you use commands such as `docker run`, the client sends this commands to `dockerd`, which carries them out.
- The `docker` command uses the Docker API
- The Docker client can communicat with more than on daemon.

#### The Docker Desktop
- is an easy-to-install application that enables you to build and share containerized applications and microservices.
- includes `dockerd`, `docker`, Docker Compose, Docker Content Trust, Kubernates, and Credential Help.

#### Docker registries
- A Docker registry stores Docker images.
- Docker Hub is a public registry that anyone can use.
- Docker is configured to look for images on Docker Hub by default.
- You can run your own private registry.
- When you use `docker run`, `docker pull` commands, the required images are pulled from your congigured registry.
- When you use `docker push`, your images is pushed to your configured registry.

#### Docker objects

> when you using Docker, you are creating and using images, containers, netwroks, volumns, plugins, and other objects.

##### Images.
> An image is read-only template with instructions for creating a Docker container.
- Often, an image is based on other image, with some additional customization.
- For example, you may build an image which is based on `ubuntu` image, but installs the Apache web server and your application,
- as well as the configuration details needed to run make your application run.
- to build your own image, you create a Dockerfile with a simple syntax for defining the steps needed to create the image and run it.
- Each instruction in a Dockerfile creates a layer in the image.
- When you change the Dockerfile and rebuild the image, only those layers which have changed are rebuilt.
- This is part of what makes images so lightweight, small and fast, when compared to other virtualization technologies.

##### Containers.
> a container is a runnable instance of an image.
- you can create, start, stop, remove, or delete a container using the Docker API or CLI.
- you can connect a container to one or more networks, attach storage to it, or even create a new image based on its current state.
- by default, a container is relatively well isolated from other containers and its host machine.
- you can control how isolated a container's network, storage, or other underlying subsystems are from other containers or from the host machine.
- a container is defined by its image as well as any configuration options you provided to it when you create or start it.
- When a container removed, any changes to its state that are not stored in persistent storage disappear.


### Example `docker run` command
- the following command runs and `ubuntu` container, attaches interactively to your local command-line session, and runs `/bin/bash`
`docker run -i -t ubuntu /bin/bash`

- when you run this command, the fllowing happens (using the default registry configuration)
1. If you do not have the `ubuntu` image locally, Docker pulls it from your congigured registry, as though you had run `docker pull ubuntu` manually.
2. Docker create a new container, as though you had run a `docker container create`  command manually.
3. Docker allocates a read-write filesystem to the container, as its final layer.
   This allows the container to create or modify files and directories in its local filesystem.
4. Docker creates a network interface to connect the container to the default network.
   since you did not specify any networking options. This includes assigning an IP address to the container.
   By default, containers can connect to external networks using the host machine's network connection.
5. Docker starts the container and executes `/bin/bash`. Because the container is running interactively and attached to your terminal (due to the `-i`, `-t` flags)
   you can provide input using your keyboard while the output is logged to your terminal.
6. When you type `exit` to terminate the `/bin/bash` command, the container stops but is not removed. you can start it again or remove it.

### The underlying technology

- writting in `Go`
- Docker uses a technology called `namespace` to provide the isolated workspace called the container.
- When you run a container, Docker creates a set of namepsace for that container.

> These namespaces provide a layer of isolation. Each aspect of a container runs in a separate namespace and its access is limited to that namespace.
