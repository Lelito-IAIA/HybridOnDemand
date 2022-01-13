# HybridOnDemand
create a LINODE WEST-CENTRAL (LONDON)!

## Clone this repository and the Marcel Dampers repo
Clone this repo to copy all the stuff needed to run.<br/>
`git clone https://github.com/Lelito-IAIA/HybridOnDemand.git`<br/>
git username: `Lelito-IAIA`<br/>
<<<<<<< HEAD
git accesstocken `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`<br/>
=======
git accesstocken `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`<br/>
>>>>>>> 6a5dffa (update 13/01/2022)

Clone the Marcel Dumper repo to copy all the sutff needed to run his Istio project.

`git clone https://github.com/marcel-dempers/docker-development-youtube-series.git`

Run the following commands to give execute permissions
```
cd HybridOnDemand

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
## Create an EKS-ANYWHERE cluster
```
CLUSTER_NAME=dev-cluster 

eksctl anywhere generate clusterconfig $CLUSTER_NAME \
   --provider docker > $CLUSTER_NAME.yaml 

   eksctl anywhere generate clusterconfig $CLUSTER2 \
   --provider docker > $CLUSTER2.yaml 

eksctl anywhere create cluster -f $CLUSTER_NAME.yaml

eksctl anywhere create cluster -f $CLUSTER1.yaml


export KUBECONFIG=${PWD}/${CLUSTER_NAME}/${CLUSTER_NAME}-eks-a-cluster.kubeconfig

kubectl get ns
```
Remember that when you will open any terminal you will need to run the following command to have the necessary environment variable to run kubectl command

```
CLUSTER_NAME=dev-cluster

export KUBECONFIG=${PWD}/${CLUSTER_NAME}/${CLUSTER_NAME}-eks-a-cluster.kubeconfig
```
## Istio part
The following command are necessary to run the demo part of Istio.

```
curl -L https://istio.io/downloadIstio | sh -

cd istio-1.12.1

export PATH=$PWD/bin:$PATH

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
`sudo apt-get update && sudo apt-get -y upgrade`

`sudo apt-get -y install xfce4`

`apt-get -y install firefox`

`sudo startxfce4`





<!-- kubectl config get-contexts


export MGMT_CLUSTER=cluster1
export MGMT_CONTEXT=cluster1-admin@cluster1
export REMOTE_CLUSTER=cluster2
export REMOTE_CONTEXT=cluster2-admin@cluster2


   CLUSTER_1_INGRESS_ADDRESS=$(kubectl --context $REMOTE_CONTEXT get svc -n istio-system istio-ingressgateway -o jsonpath='{.status.loadBalancer.ingress[0].hostname}')
   echo http://$CLUSTER_1_INGRESS_ADDRESS/productpage
   


kubectl apply \
    -f samples/helloworld/helloworld.yaml \
    -l version=v2 -n sample

    kubectl get pod -n sample -l app=helloworld

samples/multicluster/gen-eastwest-gateway.sh \
    --mesh mesh1 --cluster MGMT_CONTEXT --network network1 | \
    istioctl install -y -f -

kubectl get svc istio-eastwestgateway -n istio-system

 kubectl apply -n istio-system -f \
    samples/multicluster/expose-istiod.yaml
istioctl x create-remote-secret \
    --name=cluster2 | \
    kubectl apply -f 

    istioctl install --context="${MGMT_CONTEXT}" -f cluster1.yaml

kubectl apply --context="${MGMT_CONTEXT}" -n istio-system -f \
    samples/multicluster/expose-istiod.yaml

samples/multicluster/gen-eastwest-gateway.sh \
    --mesh mesh1 --cluster cluster1 --network network1 | \
    istioctl --context="${MGMT_CONTEXT}" install -y -f -

    istioctl x create-remote-secret \
    --context="${REMOTE_CONTEXT}" \
    --name=cluster2 | \
    kubectl apply -f - --context="${MGMT_CONTEXT}"

export DISCOVERY_ADDRESS=$(kubectl \
    --context="${MGMT_CONTEXT}" \
    -n istio-system get svc istio-eastwestgateway \
    -o jsonpath='{.status.loadBalancer.ingress[0].ip}')

istioctl install --context="${REMOTE_CONTEXT}" -f cluster2.yaml









export MGMT_CLUSTER=mgmt-cluster
export REMOTE_CLUSTER1=cluster-1
export REMOTE_CLUSTER2=cluster-2

## Quick start gloo mesh

export MGMT_CONTEXT=kind-mgmt-cluster
export REMOTE_CONTEXT1=kind-cluster-1
export REMOTE_CONTEXT2=kind-cluster-2 




kind create cluster --name mgmt-cluster
kind create cluster --name cluster-1
kind create cluster --name cluster-2

kubectl config get-contexts

export MGMT_CLUSTER=lke48716
export REMOTE_CLUSTER1=lke48717
export REMOTE_CLUSTER2=lke48718


export MGMT_CONTEXT=lke48716-ctx
export REMOTE_CONTEXT1=lke48717-ctx
export REMOTE_CONTEXT2=lke48718-ctx 



cat << EOF | kubectl --context ${MGMT_CONTEXT} apply -f -
apiVersion: networking.enterprise.mesh.gloo.solo.io/v1beta1
kind: VirtualDestination
metadata:
 name: reviews-global
 namespace: gloo-mesh
spec:
 hostname: reviews.global
 port:
   number: 9080
   protocol: http
 localized:
   outlierDetection:
     consecutiveErrors: 1
     maxEjectionPercent: 100
     interval: 5s
     baseEjectionTime: 120s
   destinationSelectors:
   - kubeServiceMatcher:
       labels:
         app: reviews
 virtualMesh:
   name: virtual-mesh
   namespace: gloo-mesh
EOF








 -->


