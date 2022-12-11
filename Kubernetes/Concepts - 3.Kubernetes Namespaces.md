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

<img width="650" alt="image" src="https://user-images.githubusercontent.com/35073431/206936378-b2de3e3d-1198-41a7-ad17-c2fdd770798e.png">

2. using config file

![image](https://user-images.githubusercontent.com/35073431/206932486-4e32fcce-8002-4b98-a4b0-a7932c98fb0e.png)


### what are the use cases
![image](https://user-images.githubusercontent.com/35073431/206932579-5f636ab0-6793-4543-b316-83501698a928.png)

![image](https://user-images.githubusercontent.com/35073431/206932670-18e7d144-2638-4010-a588-f45a244e0c76.png)

![image](https://user-images.githubusercontent.com/35073431/206932726-b418a71c-5f03-4bd0-bf58-cf80343f32e4.png)

![image](https://user-images.githubusercontent.com/35073431/206932800-2c835777-074f-4bf4-bc9d-2b8081c14003.png)


### how Namespaces work and how to uses it
1. kubectl apply -f mysql-configmap.yaml --namespace=may-namespace
2. metadata: namespace

![image](https://user-images.githubusercontent.com/35073431/206933149-19fce7a2-dc20-4c51-b29e-3a4a49cba670.png)

