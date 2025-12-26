# Getting Started

## Quick Start

This link help to deploy [ArgoCD](https://argo-cd.readthedocs.io/en/stable/getting_started/).

Create new namespace
```shell
kubectl create namespace argocd
```

Apply ArgoCD configurations
```shell
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Patch service to run locally
```shell
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```

Get ArgoCD Admin password
```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```

Run locally using Port-Forward
```shell
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

Annotate in ArgoCD Server
```shell
kubectl annotate service argocd-server -n argocd service.beta.kubernetes.io/azure-load-balancer-internal-subnet="<<SUBNET_NAME>>"
``` 

Annotate in ArgoCD Server
```shell
kubectl annotate service argocd-server -n argocd service.beta.kubernetes.io/azure-load-balancer-internal="true"
``` 

Restart ArgoCD Server and ArgoCD Dex Server
```shell
kubectl rollout restart deployment argocd-server -n argocd
kubectl rollout restart deployment argocd-dex-server -n argocd
```