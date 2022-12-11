## What is Kubernetes?
Opensource container orchestration tool

## Why we need need Kubernetes
1.	Trend from Monolith to Microservices
2.	Increased usage of containers
3.	A proper way to manage hundreds of containers

## What Kubernetes offer?
1.	High availability or no downtime
2.	Scalability / high performance
3.	Disaster recovery -backup and restore

## Kubernetes components
### Pod: 
- smallest unit of K8s
- Abstraction over container
- Usually 1 application per pod
- Each pod gets its own IP address
- New IP address on re-creation
### Service:
- Permanent IP address
- Lifecycle of pod and Service Not connected
### Ingress: 
manages external access to the services in a cluster, typically HTTP,Route traffic into the cluster
### ConfigMap: 
external configuration of your application
### Secret: 
used to store secret data, base64 encoded
### Volumes: 
storage on local machine,or remote outside of K8s cluster
### statefulSet: 
for stateful apps or databases
### Deployment: 
for stateless apps

## Kubernetes Architecture
- Each Node has multiple Pods on it
- 3processes must be installed on every Node: 1. container runtime 2. Kubelet 3. Kube proxy
- 4 processes run on every master node:1. 
API server 2. Scheduler 3.controller manager 4.etcd(key value store: cluster brain)

## Example cluster set-up
2 master nodes and 3 worker nodes

## Add new Master/Node server
1.	Get new bare server
2.	Install all the master/worker node processes
3.	Add it to the cluster

## Mini Cube: 
master and node processes run on ONE machine. One node K8s cluster runs in a virtualbox on your laptop for testing purposes

## What is kubectl?
Command line tool for K8s cluster


