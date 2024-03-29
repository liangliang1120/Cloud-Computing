![image](https://user-images.githubusercontent.com/35073431/206891968-815c978e-b5e2-4399-bd1f-edaca65daacf.png)

![image](https://user-images.githubusercontent.com/35073431/206891983-94aa92b2-0dae-4cd6-be68-e58b798ab462.png)

## MongoDB
<img width="634" alt="image" src="https://user-images.githubusercontent.com/35073431/206892225-35d4d469-ab12-40d1-b5c6-80cf5558929c.png">

- use editor to paste a prepared depoyment file
mongo.yaml
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongodb-deployment
  labels:
    app: mongodb
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mongodb
  template:
    metadata:
      labels:
        app: mongodb
    spec:
      containers: 
      - name: mongodb
        image: mongo
        ports:
        - containerPort: 27017
        env:
        - name: MONGO_INITDB_ROOT_USERNAME
          value:
        - name: MONGO_INITDB_ROOT_PASSWORD
          value:

```

we can check the mongo port,environment variables by searching in Docker website
![image](https://user-images.githubusercontent.com/35073431/206892490-e76a67be-02a3-4507-be1d-72e84e87f837.png)

![image](https://user-images.githubusercontent.com/35073431/206892531-c3917d7d-50b6-4c93-bde8-1d3716b549d1.png)

![image](https://user-images.githubusercontent.com/35073431/206892549-7043aa43-2675-4514-b05d-c8f2dec22958.png)

![image](https://user-images.githubusercontent.com/35073431/206892594-13321a47-c2b7-4f1f-80d3-f81474670d2c.png)

- Secret file
mongo-scret.yaml
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mongodb-secret
type: Opaque
data:
  mongo-root-username: dXNlcm5hbWU=
  mongo-root-password: cGFzc3dvcmQ=
```
get encoded username and password: echo -n 'username' |base64

<img width="494" alt="image" src="https://user-images.githubusercontent.com/35073431/206893283-682df7f9-cbe7-49cc-ade1-aec4935254f7.png">

- apply files
-  kubectl apply -f mongo-secret.yaml
-  kubectl get secret
-  
<img width="562" alt="image" src="https://user-images.githubusercontent.com/35073431/206893691-bb45a1b5-df41-497c-9ced-77f3e7220f27.png">

- go back to mongo.yaml
- 
<img width="375" alt="image" src="https://user-images.githubusercontent.com/35073431/206893834-5f9c0dfa-6e85-4b30-979e-a5304cc77031.png">

![image](https://user-images.githubusercontent.com/35073431/206893713-5a9b846d-00e3-4bba-b649-ead67290f4fd.png)

- apply the yaml
- kubectl apply -f mongo.yaml

<img width="592" alt="image" src="https://user-images.githubusercontent.com/35073431/206893898-38a5b2da-ccab-4f86-82de-e36b1a7905b2.png">

- yaml can contain multiple documents in one file
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongodb-deployment
  labels:
    app: mongodb
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mongodb
  template:
    metadata:
      labels:
        app: mongodb
    spec:
      containers: 
      - name: mongodb
        image: mongo
        ports:
        - containerPort: 27017
        env:
        - name: MONGO_INITDB_ROOT_USERNAME
          valueFrom:
            secretKeyRef:
              name: mongodb-secret
              key: mongo-root-username
        - name: MONGO_INITDB_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mongodb-secret
              key: mongo-root-password
---
apiVersion: v1
kind: Service
metadata:
  name: mongodb-service
spec:
  selector:
    app: mongodb
  ports:
    - protocol: TCP
      port: 27017
      targetPort: 27017
```
- apply the yaml again
- kubectl apply -f mongo.yaml

<img width="663" alt="image" src="https://user-images.githubusercontent.com/35073431/206894184-7de9b7fc-079d-4602-b0c8-fe3f36c4919d.png">


## MongoExpress
mongo-express.yaml
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongo-express
  labels:
    app: mongo-express
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mongo-express
  template:
    metadata:
      labels:
        app: mongo-express
    spec:
      containers:
      - name: mongo-express
        image: mongo-express
        ports:
        - containerPort: 8081
        env:
        - name: ME_CONFIG_MONGODB_ADMINUSERNAME
          valueFrom:
            secretKeyRef:
              name: mongodb-secret
              key: mongo-root-username
        - name: ME_CONFIG_MONGODB_ADMINPASSWORD
          valueFrom: 
            secretKeyRef:
              name: mongodb-secret
              key: mongo-root-password
        - name: ME_CONFIG_MONGODB_SERVER
          valueFrom: 
            configMapKeyRef:
              name: mongodb-configmap
              key: database_url
---
apiVersion: v1
kind: Service
metadata:
  name: mongo-express-service
spec:
  selector:
    app: mongo-express
  type: LoadBalancer  
  ports:
    - protocol: TCP
      port: 8081
      targetPort: 8081
      nodePort: 30000

```
- nodePort: Port for external IP address, Port you need to put into browser （300000-32767）


mongodb-configmap.yaml
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: mongodb-configmap
data:
  database_url: mongodb-service
```
- kubectl apply -f mongo-configmap.yaml
- kubectl apply -f mongo-express.yaml
- kubectl get pod
- kubectl logs mongo-express-5bf4b56f47-hkp86
- kubectl get service

- cluster IP will give the service an internal IP address
- loadBalancer will give interal IP address, in addition to that, will also give external IP address


<img width="740" alt="image" src="https://user-images.githubusercontent.com/35073431/206930364-b9120790-7e14-4e89-9491-a89326e90d53.png">

- minikube service mongo-express-service


<img width="737" alt="image" src="https://user-images.githubusercontent.com/35073431/206930979-10e2b5b3-9c92-4718-b026-09d49e442690.png">

<img width="1175" alt="image" src="https://user-images.githubusercontent.com/35073431/206931043-cb9e8a05-23ef-4de3-9f73-7bfa699f687e.png">


![image](https://user-images.githubusercontent.com/35073431/206931017-b1b0edc4-ee97-4bfe-89b3-10201cee3da6.png)


