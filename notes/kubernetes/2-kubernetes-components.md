Cluster
: when you deploy Kubernetes, you get a cluster

Nodes
: A Kubernetes cluster consists of a set of worker machines, called nodes
: that run containerized applications
: Every cluster has at least one worder node
: a node may be virtual or physical machine

Pods
: the worker node(s) host the Pods that are the components of the application workload
: Pods are the smallest deployable units of computing that you can create and manage in Kubernetes
: a Pod (as in a pod of whales or pea pod) is a group of one or more containers with shared storage and network resouces 
: and a specification for how to run containers
: a pod's contents are always co-located, co-scheduled, and run in a shared context.
: a pod models an application-specific logical host: contains one or more applicaton containers which are relatively tightly coupled.

Control Plane
: the control plane manages the worker nodes and the Pods in the cluster.
: in production environments, the control plane usually run across multiple computers and a cluster usually runs multiple nodes.
: provides fault-tolerance and high availability.

### Control Plane Components
- the control plane's components make global desicions about the cluster (for example, scheduling)
- as well as detecting and responding to cluster events (for example, starting up a new pod when a deployment's replicas field is unsatisfied)
- control plane components can be run on any machine in the cluster.
- however, for simplicity, set up scripts typically start all control plane components on the same machine
- and do not run user containers on this machine

#### kuber-apiserver
- the api server is a component of the Kubernetes control plane that exposes the Kubernetes API
- the api server is the front end for the Kubernetes control plane
- the main implementation of a Kubernetes API server is `Kube-apiserver`, Kube-apiserver is designed to scale horizontally
- that is, it scales by deploying more instances
- you can run serveral instances of kuber-apiserver, and balance traffic between those instances

#### etcd
- consistent and highly-available key value store used as Kubernetes' backing store for all cluster data.
- if your Kubernetes cluster uses etcd as its backing store, make sure you have a back up plan for those data.

#### kube-scheduler
- control plane component that watches for newly created Pods with no assigned node, and select a node for them to run on.
- Factors taken into account for scheduling decisions include:
: individual and collective resource requirements
: hardward/software/policy constraints
: affinity and anti-affinity specifications
: data locality
: inter-workload interference
: deadlines

#### kube-controller-manager
> that runs controller processes
- logically, each controller is a separate process
- but to reduce complexity, they are all compiled into a single binary and run in a single process.
- some types of these controllers are:
: Node controller - responsible for noticing and responding when nodes goes down.
: Job controller - watches for Job objects that responsible one-off tasks, then creates Pods to run those tasks to completion
: Endpoints controller - populates the Endpoints objects (that is, joins Services & Pods)
: service Account & Token controllers - create default accounts and API access tokens for new namespaces
