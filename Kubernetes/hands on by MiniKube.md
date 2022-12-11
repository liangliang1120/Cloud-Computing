All the crud operations happends on the deployment level
### Create pot, we create the deployment
- kubectl create deployment nginx-depl --image=nginx

<img width="458" alt="image" src="https://user-images.githubusercontent.com/35073431/206887384-6af592ad-0324-4703-9df8-c06730a69504.png">

Deployment manages a ReplicaSet
ReplicaSet manages all the replicas of that pod
Pod is an abstraction of a container

we will edit image in deployment directly not a pod:
- kubectl edit deployment nginx-depl

we get auto-generate config file with default value

<img width="621" alt="image" src="https://user-images.githubusercontent.com/35073431/206887462-57edb9c2-c06e-4686-90eb-e8c3bf12779e.png">

### debugging pods
- kubectl create deployment mongo-depl --image=mongo
- kubectl get pod
- kubectl logs mongo-depl-8fbdb868c-qbjxp
- kubectl describe pod  mongo-depl-8fbdb868c-qbjxp
- kubectl exec -it mongo-depl-8fbdb868c-qbjxp -- bin/bash (inside it as a root user)
<img width="617" alt="image" src="https://user-images.githubusercontent.com/35073431/206887885-bd20e47f-2878-4696-92b9-45c5cdaf4e48.png">
<img width="621" alt="image" src="https://user-images.githubusercontent.com/35073431/206887922-f0d9adb0-22c8-419a-8e13-be1670abfede.png">
<img width="667" alt="image" src="https://user-images.githubusercontent.com/35073431/206888031-1a951e09-9dd8-4b1f-aa02-f2f5fa2de9ea.png">

### delete deployment
- kubectl get deployment
- kubectl get pod
- kubectl delete deployment mongo-depl

<img width="719" alt="image" src="https://user-images.githubusercontent.com/35073431/206888213-1c809763-20c9-46fa-acb8-5f133faa76e5.png">


### apply config file
why? It s impractical to write all the options on a command line, so usually use kubernetes configuration files
- touch ngix-deployment.yaml
- vim ngix-deployment.yaml
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers: 
      - name: nginx
        image: nginx:1.16
        ports:
        - containerPort: 80
```
- kubectl apply -f nginx-deployment.yaml

<img width="579" alt="image" src="https://user-images.githubusercontent.com/35073431/206890112-1202a9e7-81b3-413a-8031-822ca8a225f9.png">


![image](https://user-images.githubusercontent.com/35073431/206890319-39819a46-7966-4294-8a74-cbb1dbbf8543.png)

![image](https://user-images.githubusercontent.com/35073431/206890331-07322985-fd14-40c9-903d-02a7dd99232d.png)




