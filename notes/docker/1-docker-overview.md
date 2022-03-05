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

