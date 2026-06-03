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
kubectl run -i -tty load-generator --image=busybox -n apache /bin/sh
->
  while True; do wget -q -O- https://apache-service.apache.svc.cluster.local; done

# To install metrices
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
kubectl edit deployment metrics-server -n kube-system
  ADD
  - --kubelet-insecure-tls
kubectl rollout restart deployment metrics-server -n kube-system
