### what is a namespaces
- organize resources in namespaces
- virtual cluster inside a Kubernetes cluster

### 4 Namespaces per Default
- kube-system: 
- 1. DO NOT create or modify; 
- 2.system process; 
- 3. Master or kubectl process
- kube-public: publicely accessible data; a configmap which contains cluster infomation
- kube-node-lease: heartbeat of nodes; each node
- 

### what are the use cases

### how Namespaces work and how to uses it