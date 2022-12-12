![image](https://user-images.githubusercontent.com/35073431/206939397-6830b3f7-eb48-42b9-a6ed-b410a58491d8.png)

### storage reuirements
1. storage that dosnot depend on pod lifecycle
2. storage must be available on all nodes
3. storage needs to survive even if cluster crashes

### Persistent Volume
- a cluster resource
- created via YAML file
- Persistent Volume are not namespaced
- depending on storage type spec attributes differ

![image](https://user-images.githubusercontent.com/35073431/206942202-b72b79da-6233-4c8e-89c3-f3894d3a74c9.png)

![image](https://user-images.githubusercontent.com/35073431/206942218-fdc37280-7f13-487a-90d4-320b24f5db55.png)


### Persistent Volume Claim

![image](https://user-images.githubusercontent.com/35073431/206942553-a0088fa4-404d-4374-9f4e-b2849a1abfcd.png)

![image](https://user-images.githubusercontent.com/35073431/206942589-8a683eb6-97a5-4601-8f4c-087df0839499.png)

![image](https://user-images.githubusercontent.com/35073431/206942640-7c935dc8-ad52-4dd1-b7ee-612580b9253c.png)

![image](https://user-images.githubusercontent.com/35073431/206942660-b663a968-cc1d-40d4-96aa-f813f4d6f7c3.png)

### ConfigMAp and Secret
- local volumes
- not created via PV or PVC
- managed by Kubernetes

### Storage Class
- SC provisions PV dynamically when PVC claims it
- 
![image](https://user-images.githubusercontent.com/35073431/206943370-11577365-6249-4733-87f4-82cace040220.png)

