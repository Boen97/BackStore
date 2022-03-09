### Container orchestration.

- running contains in production is tough.
- you don't want to log into a machine and simply run a `docker run` or `docker-compose up`.
- what happens if the container die?
- How do you scale across serveral machines?
- Container orchestration solves this problem.
- Tools like Kubernates, Swarm all in slightly different ways.

> The general idea is that you have "managers" who receive **expected state**
- this state might be I want to run two instances of my web app and export port 80
- the manage then look at all of the machines in the cluster and delegate work to worker nodes.
- the manager watch for changes (such as container quitting) and then work to make actual state reflect the expected state.

### Cloud Native Computing Foundation Projects

- The CNCF is a vendor-neutral home for various open-source projects, including Kubernetes, Prometheus, Envoy, Linkerd, NATS, and more! 
