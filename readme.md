# Coding helper devops

## Create local cluster
```
k3d cluster create 195063 -p 80:80@loadbalancer -p 443:443@loadbalancer -p 7687:7687@loadbalancer -p 5432:5432@loadbalancer --k3s-arg "--disable=traefik@server:*"
```

## Init
```
kubectl apply -f devops-tools/namespace.yaml
kubectl apply -f devops-tools/nginx/
kubectl apply -f devops-tools/jenkins/

kubectl apply -f db/namespace.yaml
kubectl apply -f db/core-db/
kubectl apply -f db/forum-db/

kubectl apply -f app/namespace.yaml
kubectl apply -f app/iam/
kubectl apply -f app/core/
kubectl apply -f app/forum/
```

## Get jenkins password
```
kubectl logs deployment/jenkins -c jenkins -n devops-tools | grep pass -A 3
kubectl exec -i <pod-id> -n devops-tools -c jenkins -- cat var/jenkins_home/secrets/initialAdminPassword
```