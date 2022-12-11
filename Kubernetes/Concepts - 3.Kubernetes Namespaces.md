### what is a namespaces
- organize resources in namespaces
- virtual cluster inside a Kubernetes cluster

### 4 Namespaces per Default
- kube-system: 
  - DO NOT create or modify; 
  - system process; 
  - Master or kubectl process
- kube-public: 
  - publicely accessible data; 
  - a configmap which contains cluster infomation
- kube-node-lease: 
  - heartbeat of nodes; 
  - each node has associated lease object in namespace
  - determines the availability of a node
- default
  - resources you create are located here

![image](https://user-images.githubusercontent.com/35073431/206932336-9355c71b-a747-489a-b867-120ac9cf438a.png)
### how to create your namespaces
1. kubectl create namespace [name]
   kubectl get namespace
2. using config file

![image](https://user-images.githubusercontent.com/35073431/206932486-4e32fcce-8002-4b98-a4b0-a7932c98fb0e.png)


### what are the use cases

### how Namespaces work and how to uses it
