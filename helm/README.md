# Transformers Helmified

## Helm

This directory shows how to deploy the transformers using helm (https://docs.helm.sh/).

## How to Run

Provided we've already built the docker images for minikube (see parent README) we can install install all four to minikube with:

`helm install ./transformer/ --name=optimus1 --set transformer.name=optimus-prime,image.repository=transformers/optimus-prime,service.port=30080` <br/>
`helm install ./transformer/ --name=gears1 --set transformer.name=gears,image.repository=transformers/gears,service.port=30081` <br/>
`helm install ./transformer/ --name=megatron1 --set transformer.name=megatron,image.repository=transformers/megatron,service.port=30082` <br/>
`helm install ./transformer/ --name=shockwave1 --set transformer.name=shockwave,image.repository=transformers/shockwave,service.port=30083` <br/>

And open them with (note here all default to disguised):

`minikube service optimus1-transformer`<br/>
`minikube service gears1-transformer`<br/>
`minikube service megatron1-transformer`<br/>
`minikube service shockwave1-transformer`<br/>

Transform them with:

`helm upgrade optimus1 --set transformer.mode=robot,transformer.name=optimus-prime,image.repository=transformers/optimus-prime,service.port=30080 --recreate-pods ./transformer/` <br/>
`helm upgrade gears1 --set transformer.mode=robot,transformer.name=gears,image.repository=transformers/gears,service.port=30081 --recreate-pods ./transformer/` <br/>
`helm upgrade megatron1 --set transformer.mode=robot,transformer.name=megatron,image.repository=transformers/megatron,service.port=30082 --recreate-pods ./transformer/` <br/>
`helm upgrade shockwave1 --set transformer.mode=robot,transformer.name=shockwave,image.repository=transformers/shockwave,service.port=30083 --recreate-pods ./transformer/` <br/>

Note this takes a little time but if you refresh browser (preferably with private browsing - or run the four minikube service commands again)  in theory you should see it reflected without downtime (currently that's not guaranteed at the time of writing due to https://github.com/kubernetes/helm/issues/1702 and https://github.com/kubernetes/kubernetes/issues/55667).

And delete with:

`helm del --purge optimus1`<br/>
`helm del --purge gears1`<br/>
`helm del --purge megatron1`<br/>
`helm del --purge shockwave1`<br/>