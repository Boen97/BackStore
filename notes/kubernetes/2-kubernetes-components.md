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
