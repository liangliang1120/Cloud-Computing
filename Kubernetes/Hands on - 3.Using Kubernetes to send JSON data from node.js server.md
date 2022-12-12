## Step 1: Creating running and sharing a container image
1. Go to GCP and open the terminal

<img width="1315" alt="image" src="https://user-images.githubusercontent.com/35073431/206944779-95a9d4ab-829c-43c9-9929-0bc55a2bfdc6.png">

2. Check Zonal support for Intel Haswell platform
- gcloud compute zones describe us-west2-a

<img width="749" alt="image" src="https://user-images.githubusercontent.com/35073431/206944880-92b08e78-378b-44ab-b0e9-2f5d367fe9a5.png">

3. Create a boot disk which is really a staging disk
- gcloud compute disks create stagingdisk --image-project centos-cloud --image-family centos-7 --zone us-west2-a

<img width="1212" alt="image" src="https://user-images.githubusercontent.com/35073431/206945078-b694798e-3136-4286-8ec7-e323ec0a223a.png">

4. Create a nested VM 
- gcloud compute images create nested-vm-image --source-disk=stagingdisk --source-disk-zone=us-west2-a --licenses=https://www.googleapis.com/compute/v1/projects/vm-options/global/licenses/enable-vmx

<img width="1304" alt="image" src="https://user-images.githubusercontent.com/35073431/206945376-42be2abe-0c6f-4850-8f4f-81bd037a6250.png">

5. Delete the source disk we created temporarily as a staging disk.
-  gcloud compute disks delete stagingdisk --zone us-west2-a

<img width="906" alt="image" src="https://user-images.githubusercontent.com/35073431/206945611-2bae95c1-8046-46dd-bc9a-c9ad31abc35a.png">

6. Create Image
- gcloud compute instances create nested-vm-image1 --zone us-west2-a --min-cpu-platform "Intel Haswell" --machine-type n1-standard-4 --image nested-vm-image

<img width="1158" alt="image" src="https://user-images.githubusercontent.com/35073431/206946108-5cc49323-e833-4d30-b9c5-a287cb4db7b8.png">

7. Connect to VM, selecting Open in Browser window and verify the VM is online

<img width="1366" alt="image" src="https://user-images.githubusercontent.com/35073431/206946237-7f61a745-6d41-4416-a6bf-03843e7cda5f.png">

- grep -cw vmx /proc/cpuinfo
grep -cw vmx /proc/cpuinfo

<img width="895" alt="image" src="https://user-images.githubusercontent.com/35073431/206946370-2e80cf91-0e30-46e4-9fa4-15be7c3ba65f.png">

8. Install kubectl
- sudo yum install -y kubectl
- 
<img width="874" alt="image" src="https://user-images.githubusercontent.com/35073431/206946551-a5380b68-9d8d-4baa-93dc-e2aec2602b28.png">

<img width="876" alt="image" src="https://user-images.githubusercontent.com/35073431/206946586-59dac3a1-ef08-4911-bccd-3fda84396816.png">


9. Make a directory, change Permissions and move to your /usr/bin directory
- mkdir kubectl
- chmod +x kubectl
- sudo mv ./kubectl /usr/local/bin/kubectl

<img width="526" alt="image" src="https://user-images.githubusercontent.com/35073431/206946684-d072dc87-79b4-429a-9488-fc8dc356303e.png">

10. Install Virtualbox kernel
- sudo yum install kernel-devel kernel-headers make patch gcc wge

<img width="844" alt="image" src="https://user-images.githubusercontent.com/35073431/206947263-3c36c357-5354-40f8-9b50-b751d386d4e7.png">

<img width="1008" alt="image" src="https://user-images.githubusercontent.com/35073431/206947294-313b4781-91a0-4597-b959-c2941b0c02b8.png">

11. Download Virtualbox sudo wget
- sudo yum install wget
-  sudo wget https://download.virtualbox.org/virtualbox/rpm/el/virtualbox.repo -P /etc/yum.repos.d
-  
<img width="960" alt="image" src="https://user-images.githubusercontent.com/35073431/206947751-958ca8e9-449f-46ec-bde0-09a315c27a9e.png">

12. Install Virtualbox sudo yum install VirtualBox-6.0
- sudo yum install VirtualBox-6.0

<img width="926" alt="image" src="https://user-images.githubusercontent.com/35073431/206948353-eabb6bea-d9f1-4f9e-befd-b40757077d52.png">

13. Download and Install Minikube
- curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube

<img width="1009" alt="image" src="https://user-images.githubusercontent.com/35073431/206948446-b222ba4a-9699-467a-9134-8a62259608fc.png">

14. CP to directory.
-  sudo cp minikube /usr/bin/

<img width="440" alt="image" src="https://user-images.githubusercontent.com/35073431/206948530-1879d6fc-4026-4072-a785-1c139122faaa.png">

15. Docker needs to be installed
-sudo yum install docker sudo yum install docker

<img width="589" alt="image" src="https://user-images.githubusercontent.com/35073431/206948819-a911b82d-684f-451a-b676-2e18335a08f5.png">

16. Start Docker and install conntrack:
- sudo service docker start
- sudo yum install conntrack

<img width="886" alt="image" src="https://user-images.githubusercontent.com/35073431/206948921-2dbe4503-c271-4b43-87f1-03dcc604c974.png">

17. Start the MiniKube Cluster
-  minikube start

<img width="649" alt="image" src="https://user-images.githubusercontent.com/35073431/206949187-1a37de8b-ae5c-4a68-a624-f3723bbcfba7.png">

18. Check your cluster info
- kubectl cluster-info

<img width="854" alt="image" src="https://user-images.githubusercontent.com/35073431/206949529-ce467f92-9ee2-472a-92eb-119a1a8296ba.png">

19. Install vim make and go to dockerimg directory
- sudo yum install vim
- mkdir dockerimg
- cd dockerimg
- 
<img width="828" alt="image" src="https://user-images.githubusercontent.com/35073431/206949576-1befbdbb-5b9d-46f4-8a11-1ee91ab283c3.png">

20. Create Student_info.js
- vim app.js
```
const http = require('http');
const os = require('os');

console.log("Kubia server starting...");

var handler = function(request, response) {
  console.log("Received request from " 
              + request.connection.remoteAddress);
  response.writeHead(200);
  response.end("You've hit " + os.hostname() + "\n");
};

var www = http.createServer(handler);
www.listen(8080);
```

21. Edit Dockerfile:
- vim Dockerfile
```
FROM node:7
ADD app.js /app.js
ENTRYPOINT ["node", "app.js"]
```

<img width="280" alt="image" src="https://user-images.githubusercontent.com/35073431/206950610-e4ea849d-8909-477b-bbb2-579015574bdf.png">

22. Build the docker image
- sudo docker build -t kubia .

<img width="507" alt="image" src="https://user-images.githubusercontent.com/35073431/206951795-51dfed97-d153-4d06-9095-cae75ccf5796.png">


23. Run the image on a container on localhost:
- sudo docker run --name kubia-container2 -p 8080:8080 -d kubia
- sudo docker ps -a
- curl http://localhost:8080

<img width="897" alt="image" src="https://user-images.githubusercontent.com/35073431/206958074-c3cb230d-d1f7-40a2-8d57-c15ceb15fc9a.png">


Stop > $ sudo docker stop kubia-container
Start > $ sudo docker start kubia-container

24. Create a docker account
Go docker official website, create account.
Go Repositories > Create Repository

25. Tag the kubia docker image and login docker
- sudo docker tag kubia gulianglily/my-docker-repository
- sudo docker login -u="gulianglily" -p"password"

![image](https://user-images.githubusercontent.com/35073431/206959610-20aacdd1-673c-4280-88a1-3a2040bcdf67.png)

<img width="572" alt="image" src="https://user-images.githubusercontent.com/35073431/206960484-cff1232e-3ccb-4c12-a21c-d1185d26abe9.png">

26. Push the docker image to Docker Hub
- sudo docker push gulianglily/my-docker-repository

<img width="813" alt="image" src="https://user-images.githubusercontent.com/35073431/206960701-25fe020c-5961-4eee-85b6-c4a57040fafa.png">

![image](https://user-images.githubusercontent.com/35073431/206960845-42758160-7031-4718-8075-63003b888ecc.png)

## Step 2: Running the app on Kubernetes
1. Go to GCP 

<img width="1056" alt="image" src="https://user-images.githubusercontent.com/35073431/206961074-9bcef4f4-007b-4f58-aa2b-9c0ac4b7208a.png">


2. Create a Kubernetes cluster with three nodes
- gcloud container clusters create kubia --num-nodes=1 --machine-type=e2-micro --region=us-west1

<img width="1053" alt="image" src="https://user-images.githubusercontent.com/35073431/206962405-182abede-6fa1-427c-a756-cdf374b95217.png">

3. Check if nodes are correctly created
- kubectl get nodes

<img width="665" alt="image" src="https://user-images.githubusercontent.com/35073431/206962444-cb9d4ba2-5d4c-41d3-930c-b7eeffe5d30e.png">

<img width="1140" alt="image" src="https://user-images.githubusercontent.com/35073431/206962552-ab6b0792-c0b3-4ad5-b948-c17c154b20a7.png">

4. Create kubia-rc.yaml
$ vim kubia_rc.yaml
```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: kubia
spec:
  replicas: 3
  selector:
    app: kubia
  template:

    metadata:

      labels:

        app: kubia

    spec:

      containers:

      - name: kubia

        image: gulianglily/my-docker-repository

        ports:

        - containerPort: 8080
```


5. Create the ReplicationController
$ kubectl create -f kubia-rc.yaml

<img width="618" alt="image" src="https://user-images.githubusercontent.com/35073431/206966226-89989303-6154-4fa1-95ab-c6cd89cfe89c.png">

6. Check the pods created
$ kubectl get pods

<img width="474" alt="image" src="https://user-images.githubusercontent.com/35073431/206966385-05afba4d-64e0-4d77-9d81-1c4bb9002d87.png">

7. Deploy my node.js app
$ kubectl run kubia --image=gulianglily/my-docker-repository1 --port=8080

<img width="899" alt="image" src="https://user-images.githubusercontent.com/35073431/206966466-e6865451-81eb-4971-980a-559cf75f4604.png">


8. Creating a Service object
$ kubectl expose rc kubia --type=LoadBalancer --name kubia-http

9. List Services
$ kubectl get services

<img width="863" alt="image" src="https://user-images.githubusercontent.com/35073431/206966862-473ccf37-b70e-4f4b-b93c-87671eed84b1.png">


10. Accessing the service through its external IP
$ curl http://104.199.119.27:8080

![image](https://user-images.githubusercontent.com/35073431/206985252-2039e119-a8b9-48ec-a18a-a2854417ce1b.png)



