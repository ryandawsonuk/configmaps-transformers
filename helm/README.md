# Transformers Helmified

## Helm

This directory shows how to deploy the transformers using helm (https://docs.helm.sh/). Tested with helm v2.8.2 (note that 2.8.0 was affected by https://github.com/kubernetes/helm/issues/3372)

## How to Run

Provided we've already built the docker images for minikube (see parent README) we can install install all the transformers to minikube from this directory with:

`helm install --name=transformers1 ./transformers/`

And open them with:

`minikube service transformers1-optimusprime`<br/>
`minikube service transformers1-gears`<br/>
`minikube service transformers1-megatron`<br/>
`minikube service transformers1-shockwave`<br/>

Transform them with:

`helm upgrade transformers1 --recreate-pods --set autobots.mode=disguised,decepticons.mode=robot ./transformers/` <br/>

Note this takes a little while but if you refresh your browser (preferably with private browsing - or run the four minikube service commands again) you'll see it reflected without downtime.

And delete with:

`helm del --purge transformers1`