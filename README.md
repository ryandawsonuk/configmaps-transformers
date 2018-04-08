# Kubernetes ConfigMaps Transformers Example

## Aims

To demonstrate ConfigMaps by swithing Transfomer services between 'disguised' and 'robot' modes in minikube.

## Pre-requisites

Docker (https://docs.docker.com/install/) and minikube (https://kubernetes.io/docs/tasks/tools/install-minikube/) installed.

## How to Run

### First Deploy 

Start minikube:
 
`minikube start --memory 4000 --cpus 3`

Build images for Transformers - from this directory run

`eval $(minikube docker-env)` <br/>
`mvn clean install`

Deploy the Autobots (their ConfigMap has them as in robot mode)
 
`kubectl create -f autobots --save-config`

To see the autobots: 

`minikube service optimus-prime-entrypoint` <br/>
`minikube service gears-entrypoint` <br/>

Deploy the Decepticons (their ConfigMap has them disguised)
 
`kubectl create -f decepticons --save-config`

`minikube service megatron-entrypoint` <br/>
`minikube service shockwave-entrypoint` <br/>

### Changing Config

To change config there are options.

##### Option 1 - Change with small downtime

Do `minikube dashboard` to open the dashboard in the browser, go to 'Config Maps' under 'Config and Storage' and e.g. change the Decepticons to 'robot'. Then do:

`kubectl scale deployment/megatron --replicas=0;`<br />
`kubectl scale deployment/megatron --replicas=2;`<br />

##### Option 2 - Change with no downtime

Edit the .yml files for each transformer in the autobots and decepticons directories to point to v2 of the config. Then do:

`kubectl apply -f autobots --record`<br />
`kubectl apply -f decepticons --record`<br />

Note it can take a while for the rolling update to be fully applied and also beware the browser cache (and dep on your minikube version you may hit https://github.com/kubernetes/kubernetes/issues/55667).

### Remove and Stop

To remove:

`kubectl delete -f autobots` <br/>
`kubectl delete -f decepticons` <br/>

Stop minikube with `minikube stop`