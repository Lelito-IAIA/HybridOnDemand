# HybridOnDemand
LINODE WEST-CENTRAL!

git clone https://github.com/Lelito-IAIA/HybridOnDemand.git

git accesstocken ` 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 `

git clone https://github.com/marcel-dempers/docker-development-youtube-series.git

Run the following commands to give execute permissions
```
chmod +x docker.sh

chmod +x kubectl.sh

chmod +x eks.sh 
```
Run the scripts and install the necessary packages
```
./docker.sh

./kubectl.sh

./eks.sh
```
## create a cluster
```
CLUSTER_NAME=dev-cluster 

eksctl anywhere generate clusterconfig $CLUSTER_NAME \
   --provider docker > $CLUSTER_NAME.yaml 

eksctl anywhere create cluster -f $CLUSTER_NAME.yaml

export KUBECONFIG=${PWD}/${CLUSTER_NAME}/${CLUSTER_NAME}-eks-a-cluster.kubeconfig

kubectl get ns
```

## istio part
```
curl -L https://istio.io/downloadIstio | sh -

cd istio-1.12.1

export PATH=$PWD/bin:$PAT

istioctl install --set profile=demo -y

kubectl label namespace default istio-injection=enabled

kubectl apply -f samples/bookinfo/platform/kube/bookinfo.yaml

kubectl get services

kubectl get pods

kubectl apply -f samples/bookinfo/networking/bookinfo-gateway.yaml

istioctl analyze

export INGRESS_PORT=$(kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.spec.ports[?(@.name=="http2")].nodePort}')

export SECURE_INGRESS_PORT=$(kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.spec.ports[?(@.name=="https")].nodePort}')

export INGRESS_HOST=$(kubectl get po -l istio=ingressgateway -n istio-system -o jsonpath='{.items[0].status.hostIP}')

export GATEWAY_URL=$INGRESS_HOST:$INGRESS_PORT

echo "$GATEWAY_URL"

echo "http://$GATEWAY_URL/productpage"

kubectl apply -f samples/addons

kubectl rollout status deployment/kiali -n istio-system

istioctl dashboard kiali
```

## GUI installation
`sudo apt-get update && sudo apt-get upgrade`

`sudo apt-get -y install xfce4`

`apt-get -y install firefox`

`sudo startxfce4`

