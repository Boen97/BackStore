## What is Kubernetes

- Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services
- that facilitates both declarative configuration and automation.
- K8s as an abbreviation results from counting the eight letters between the 'K' and the 's'

### Going back in time

1. Traditional deployment era
   - early on, organizations ran applications on physical servers
   - there was no way to define resource boundaries for applications in a physical server.
   - this caused resource allocation issues.
   - if multiple applications run on a physical server
   - there can be instances where one application would take up most of the resources
   - as a result, the other application would underperform.
   - a solution for this would be to run each application on a different physical server.
   - but this did not scale as resources were underutilized, and it was expensive for organizations to maintain many physical servers.
   
2. Virtualized deployment era
   - as a solution, virtualization was introduced
   - it allow you to run multiple virtual machines (VMs) on a single physical server's CPU
   - virtualization allows applications to be isolated between VMs
   - and provides a level of security as the information of one application cannot be freely accessed by another application.
   - with virtualization, you can present a set of physical resources as a cluster of disposable virtual machines.
   - each VM is a full machine running all the components, including its own operating system, on top of the virtual hardware.
   
3. Container deployment era
   - containers are similar to VMs, but they have relaxed isolation properties to share the Operating System(OS) among the applications.
   - therefore, containers are considered lightweight.
   - similar to VM, containers has its own filesystem, share of CPU, memory, process space, and more.
   > as they decoupled from the underlying infrastructure, they are portable across clouds and OS distributions.
   - containers has the following benefits:
   1. Agile application create and deployment
      increase ease and efficiency of container image creation compared to VM image use.
   2. continouse development, integration, and deployment
      provides for reliable and frequent container image build and deployment with quick and efficient rollbacks (due to image immutability)
   3. Dev and Ops separation of concerns:
      create application container images at build/release time rather than deployment time
      thereby decoupling applications from infrastructure 
   4. Observability
      not only surfaces OS-level information and metrics, but also application health and other signals.
   5. Environmental consistency across development, tesing, and production
      runs the same on a laptop as it does in the cloud
   6. Cloud and OS distribution portability
   7. Application-centric management
      raises the level of abstraction from running an OS on virtual hardware to running application on an OS using logical resources.
   8. Loosely coupled, distributed, elastic, liberated micro-services:
      applications are broken into smaller, independent pieces and can be deployed and managed dynamically
      not a monolithic stack running on one big single-purpose machine.
   9. Resource isolation
      Predictable application performance
   10. Resource utilization
       high efficiency and density
  
### Why you need Kubernetes and what it can do 
  
- containers are a good way to bundle and run your applications.
- In a production environment, you need to manage the containers that run the applications and ensure that there is no downtime
- for example, if a container goes down, another container needs to start
> wouldn't it be easier if this behavior was handled by a system

> Kubernetes provides you with a framework to run distributed systems resiliently

- Kubernetes take care of scaling and failover for your application, provides deployment patterns and more.
- for example, Kubernetes can easily manage a canary deployment for your system

> Kubernetes provides you with:
1. Service Discovery and load balancing
   - Kubernetes can expose a container using the DNS name or using there won IP addresses.
   - if traffic to a container is high, Kubernetes is able to load balance and distribute the network traffic
   
2. Storage orchestration 
   - Kubernetes allows you to automatically mount a storage system of your choice, such as local storage, public cloud providers and more

3. Automated rollouts and rollbacks
   - you can describe the desired state for your deployed containers using Kubernetes.
   - it can change the actual state to the desired state at a controlled rate.
   - for example, you can automate Kubernetes to create new container for your development
   - remove existing containers and adopt all their resources to the new container.

4. Automatic bin packing
   - you provide Kubernetes with a cluster of nodes that it can use to run containerized tasks.
   - you tell Kubernetes how much CPU and memory (RAM) each container needs.
   - Kubernetes can fit containers onto your nodes to make the best use of your resources.

5. Self-healing
   - Kubernetes restarts containers that fail, replaces containers, kill containers that don't respond to your user-defined health check
   - and doesn't advertise them to clients until they are ready to serve

6. Secret and configuration management
   - Kubernetes lets you store and manage sensitive information, such as passwords, OAuth tokens, and SSH keys.
   - you can deploy and update secrets and application configuration without rebuilding your container images
   - and without exposing secrets in you stack configuration
