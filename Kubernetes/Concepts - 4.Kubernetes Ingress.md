### what is Ingress
an API object that provides routing rules to manage access to the services within a Kubernetes cluster.

### Ingress YAML configuration
![image](https://user-images.githubusercontent.com/35073431/206933679-134d5fcf-4a55-4f6e-961d-2795874676dc.png)

![image](https://user-images.githubusercontent.com/35073431/206933710-62b4f9df-8b74-45ca-9fbe-a4b454bdc86e.png)
No nodePort in internal service
default type: ClusterIP

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: dashboard-ingress
  namespace: kubernetes-dashboard
  annotations:
    kubernetes.io/ingress.class: "nginx"
spec:
  rules:
  - host: dashboard.com
    http:
      paths:
      - path: /
        pathType: Exact  
        backend:
          service:
            name: kubernetes-dashboard
            port: 
              number: 80

```
- kubectl apply -f dashboard-ingress.yaml
- kubectl get ingress -n kubernetes-dashboard
- kubectl get ingress -n kubernetes-dashboard --watch
- sudo vim /etc/hosts
- 
![image](https://user-images.githubusercontent.com/35073431/206936802-48382fa8-86d4-4236-8ff3-1cdb583d1f89.png)

![image](https://user-images.githubusercontent.com/35073431/206936871-ee214a68-2e3e-4b3e-bb87-677f63e6f6c5.png)


### when do you need Ingress

![image](https://user-images.githubusercontent.com/35073431/206937177-f4f22d70-d644-430c-b088-7297b81250b3.png)

![image](https://user-images.githubusercontent.com/35073431/206937233-c5c48c39-b881-4666-a766-b75b9f6bbb35.png)

![image](https://user-images.githubusercontent.com/35073431/206937296-878245e1-5309-49cc-8fb9-0922326014e2.png)

### Ingress controller

![image](https://user-images.githubusercontent.com/35073431/206933859-cfe7942c-48e0-427f-8300-edbb6b15b547.png)

