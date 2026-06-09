# To create nameSpace
kubectl create namespace --your-namespace-name--

# To describe details of a pod
kubectl describe pods/--podName-- -n --namespaceName--

# To enter into the shell of a container
kubectl exec -it nginx-pod -n nginx -- bash

# To apply deployment
kubectl apply -f deployment.yml

# To see the deployment
kubectl get deployment -n nginx

# To see the pods
kubectl get pods -n nginx

# To scale pods
kubectl scale deployment/nginx-deployment -n nginx --replicas=5

# To reduce to 1
kubectl scale deployment/nginx-deployment -n nginx --replicas=1

# To update or rollout update of nginx to lower version without stopping pods
kubectl set image deployment/nginx-deployment -n nginx nginx=nginx:1.27.3

# To get more details about pods
kubectl get pods -n nginx -o wide

## To apply replicasets
kubectl apply -f replicasets.yml

# To get replicasets
kubectl get replicasets -n nginx

# To get daemonsets
kubectl get daemonsets -n nginx

# To get deployment
kubectl get deployment -n nginx

# To get job
kubectl get job -n nginx

# To get persistentVolume
kubectl get pv

# To delete persistent volume
kubectl delete pv --local-pv--

# To get persistentVolumeClaim
kubectl get pvc

# To delete persistent volume claim
kubectl delete pvc --local-pvc--

# To get all
kubectl get all

# To port forward for accessing port of a container 
#In local
kubectl port-forward service/nginx-service -n nginx 80:80 --address=0.0.0.0
# 80:80 (runs on the browser : container Port)
#In EC2
sudo -E kubectl port-forward service/nginx-service -n nginx 80:80 --address=0.0.0.0
# For sudo -E it run that command in an environment

# Ingress-controller
kubectl apply -f https://kind.sigs.k8s.io/examples/ingress/usage.yaml

# To run port forward in ingress
kubectl port-forward services/ingress-nginx-controller -n ingress-nginx  9090:80 --address=0.0.0.0

# To create encrypted password
echo "password" | base64

# To apply taint to a node
kubectl taint node --nodeName-- prod=true:NoSchedule
#prod means production is true reason for doing taint

# To remove taint
kubectl taint node <nodeName> prod=true:NoSchedule-

# To avoid taint
add this to code in container scope
tolerations:
      - key: "prod"
        operator: "Equal"
        value: "true"
        effect: "NoSchedule"

# To run port-forward in background
kubectl port-forward service/nginx-service -n nginx 80:80 --address=0.0.0.0 &

# To install vpa
git clone https://github.com/kubernetes/autoscaler.git
./hack/vpa-up.sh

# TO create load-generator
kubectl run -i -t load-generator --image=busybox -n apache -- /bin/sh
->
  while true; do wget -q -O- http://apache-service.apache.svc.cluster.local; done

# To install metrices
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
kubectl edit deployment metrics-server -n kube-system
  ADD
  - --kubelet-insecure-tls
kubectl rollout restart deployment metrics-server -n kube-system

# To see the user 
kubectl auth whoami

# To use command in rback
kubectl auth can-i get deployment -n apache

kubectl auth can-i delete deployment -n apache

# Tlo get service account
kubectl get serviceaccount -n apache

# To get role
kubectl get role -n apache

# To get service account
kubectl get serviceaccount -n apache

# To get pods as an user
kubectl auth can-i get pods -n apache --as=apache-user

# TO deploy dashboard
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml

# To create token for kubernate dashboard
kubectl -n kubernetes-dashboard create token admin-user

# To run port forward for dashboard
kubectl proxy --address="0.0.0.0" --port=8001 --accept-hosts=".*"

# To access the dashboard
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login

# TO create helm chart
helm create (chartname) i.e, apache-helm

# To see the files of helm chart in a structured manner
-> install tree
   sudo apt install tree

# To change any file values of deployment, service and .. change it on values.yaml it auto changes it from all files
# To package it 
  helm package apache-helm/

# To install package
helm install fileName apache-helm

# TO uninstall or remove package
helm uninstall packageName

# To install in package in particular namespace
helm install nginxhelm nginx-helm -n nginx --create-namespace

# To upgrade any package 
-> edit in values.yaml
-> Create package
-> helm upgrade nginxhelm nginx-helm -n nginx

# To rollback previous revision
 helm rollback nginxhelm 1 -n nginx
  -> 1 is the revision which is mentioned when install package, You can move to that stage by applying revision number
# In helm chart.yaml you can upgrade the version everytime you ugrade your app

# To install istio directly
kind create cluster --name istio-testing

# To download istio
-> curl -L https://istio.io/downloadIstio | sh -
-> sudo mv istioctl /usr/local/bin



