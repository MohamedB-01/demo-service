import and just run
localhost:8080/hello
http://localhost:8080/hello

Generate the jar file by clicking maven -> package
Verify target folder - demoservice.jar 

Create docker image
docker build -t demoservice:latest .

verify 
docker images

hub.docker.com  - create an account

open a command prompt
docker login

username:
password : 

Pushing your image to central hub (docker)

---tag
docker tag demoservice:latest mbdocker001/dockerhub:demoservice


--push
docker push mbdocker001/dockerhub:demoservice

Your docker image should be in the docker hub

=======================Kubernetes
create deployments folder
Create demo-deployment.yml

apiVersion: apps/v1
kind: Deployment
metadata:
name: demo-deployment
labels:
app: demo
spec:
replicas: 6
selector:
matchLabels:
app: demo
template:
metadata:
labels:
app: demo
spec:
containers:
- name: demo
image: 8867205331/dockerhub:demoservice
ports:
- containerPort: 8080
#imagePullPolicy: Never
# livenessProbe:
# readinessProbe:

open admin cmd and navigate to the above deployments folder

kubectl get all

nothing be there except k8s service

kubectl create -f demo-deployment.yml 

Verify (wait for 1 minute)
----
kubectl get all

kubectl expose deployment demo-deployment --type=NodePort --port=8080

minikube service demo-deployment --url

Browser : 
http://192.168.59.109:30517/hello


That's it 