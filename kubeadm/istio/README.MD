# ISTIO


# To install istio directly
kind create cluster --name istio-testing

# To download istio
-> curl -L https://istio.io/downloadIstio | sh -
-> cd istio/istio-1.30.1/bin
-> sudo mv istioctl /usr/local/bin
-> Run istio_install.sh (from repo)
-> kubectl label namespace default istio-injection=enabled
# to check enabled or not
kubectl get namespace -L istio-injection
-> kubectl get crd gateways.gateway.networking.k8s.io &> /dev/null || {
  kubectl kustomize "github.com/Kubernetes-sigs/gateway-api/config/crd?ref=v1.2.0" | kubectl apply -f -
}

# Sample deploy application
kubectl apply -f samples/bookinfo/platform/kube/bookinfo.yaml
kubectl apply -f samples/bookinfo/platform/kube/bookinfo-versions.yaml
# Deploy gateway
kubectl apply -f samples/bookinfo/gateway-api/bookinfo-gateway.yaml
# Annotate gateway
kubectl annotate gateway bookinfo-gateway networking.istio.io/service-type=ClusterIP --namespace=default
# To visualize as dashboard
kubectl apply -f samples/addons/prometheus.yaml
kubectl apply -f samples/addons/kiali.yaml

# To visualize in dashboard
in ec2
kubectl port-forward svc/kiali -n istio-system 20001:20001 --address 0.0.0.0
in local
istioctl dashboard kiali


# TO request 100 times
for i in {1..100}; do   curl http://3.111.218.170:8080/productpage; done
