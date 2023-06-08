# Coding helper devops

## Create local cluster
```
k3d cluster create 195063 -p 80:80@loadbalancer -p 443:443@loadbalancer --k3s-arg "--disable=traefik@server:*"
```

## Init
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml
kubectl apply -f devops-tools/namespace.yaml
kubectl apply -f devops-tools/jenkins/pvc.yaml
kubectl apply -f devops-tools/jenkins/deploy.yaml
kubectl apply -f devops-tools/jenkins/service.yaml
kubectl apply -f devops-tools/jenkins/ingress.yaml
```

## Get jenkins password
```
kubectl logs deployment/jenkins -n devops-tools | grep pass -A 3
```