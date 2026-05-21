# To create nameSpace
kubectl create namespace <your-namespace-name>

# To describe details of a pod
kubectl describe pods/<podName> -n <namespaceName>

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
kubectl delete pv <local-pv>

# To get persistentVolumeClaim
kubectl get pvc

# To delete persistent volume claim
kubectl delete pvc <local-pvc>

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

