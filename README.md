# Kubernetes ConfigMaps Transformers Example

## Aims

To demonstrate ConfigMaps by swithing Transfomer services between 'disguised' and 'robot' modes in minikube.

## Pre-requisites

Docker (https://docs.docker.com/install/) and minikube (https://kubernetes.io/docs/tasks/tools/install-minikube/) installed.

## How to Run

Start minikube:
 
`minikube start --memory 4000 --cpus 3`

Build images for Transformers - from this directory run

`eval $(minikube docker-env)` <br/>
`mvn clean install`

Deploy the Autobots (their ConfigMap has them as in robot mode)
 
`kubectl create -f autobots`

To see the autobots: 

`open http://$(minikube ip):30080` <br/>
`open http://$(minikube ip):30081` <br/>

Deploy the Decepticons (their ConfigMap has them disguised)
 
`kubectl create -f decepticons`

`open http://$(minikube ip):30082` <br/>
`open http://$(minikube ip):30083` <br/>

To see all Transformers

`kubectl get pods`

To remove:

`kubectl delete -f autobots` <br/>
`kubectl delete -f decepticons` <br/>

Stop minikube with `minikube stop`