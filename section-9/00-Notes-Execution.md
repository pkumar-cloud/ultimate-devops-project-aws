#Deploy the application and access using LB-Type SVC
```
kubectl config current-context
kubectl get all
cd ultimate-devops-project-demo/kubernetes
kubectl apply -f serviceaccount.yaml
kubectl get sa
kubectl apply -f complete-deploy.yaml
kubectl get po, svc

kubectl edit svc opentelemetry-demo-frontend
- change svc type to LB
kubectl get svc opentelemetry-demo-frontend
<ExternalIP-FQDN>:8080


```
