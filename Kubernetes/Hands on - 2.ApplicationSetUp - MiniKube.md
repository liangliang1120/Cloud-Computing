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

Secret file

mongo-scret.yaml
```yaml
apiVersion: apps/v1
kind: Secret
  name: mongodb-secret
type: Opaque
data:
  mongo-root-username: dXNlcm5hbWU=
  mongo-root-password: cGFzc3dvcmQ=
```
get encoded username and password: echo -n 'username' |base64

<img width="494" alt="image" src="https://user-images.githubusercontent.com/35073431/206893283-682df7f9-cbe7-49cc-ade1-aec4935254f7.png">
- apply files
-- kubectl apply -f mongo-secret.yaml
## MongoExpress
