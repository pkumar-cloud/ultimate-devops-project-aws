# Deploy the services and access using LB-Type SVC
```
kubectl config current-context
kubectl get all
cd ultimate-devops-project-demo/kubernetes OR cd ultimate-devops-project-aws/section-9/k8s-manifests
kubectl apply -f serviceaccount.yaml
kubectl get sa
kubectl apply -f complete-deploy.yaml
kubectl get po, svc

kubectl edit svc opentelemetry-demo-frontendproxy
- change svc type to LB
kubectl get svc opentelemetry-demo-frontendproxy
<ExternalIP-FQDN>:8080


```
# Setup ALB ingress controller
```
eksctl version
kubectl config current-context
Follow steps: 07-alb-ingress-controller.md
```
# Setup Ingress resource for "opentelemetry-demo-frontendproxy" svc and access the project
- Make sure to delete the LB created earlier. Edit the "opentelemetry-demo-frontendproxy" and change type from Loadbalancer to Nodeport. Once saved will delete the created LB by service.
```
cd ultimate-devops-project-demo/kubernetes/frontendproxy OR cd ultimate-devops-project-aws/section-9/k8s-manifests/frontendproxy
kubectl apply -f ingress.yaml #ALB controller reads ingress resource and create a ELB
kubectl get ing
```
- To access the application, map ELB ip address to local host file, since ingress is set to only allow traffic from example.com
```
nslookup <ELB-FQDN-FromAWSConsole>
sudo vim /etc/hosts
# <IP Adress> example.com
Launch app: example.com
```
