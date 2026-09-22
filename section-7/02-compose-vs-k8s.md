# Docker Compose vs Kubernetes

### Docker Compose

### Management of Multi-Container Applications 
- Runtime execution platform for the containers.
- **Docker Compose** is ideal for **simple, single-host applications**.  
- It allows you to define and run multi-container applications with a single `docker-compose.yml` file.  
- **Docker Compose** is **best suited for development environments** and smaller-scale use cases.  

### Kubernetes

### Container Orchestration Platform
- **Kubernetes** is designed for **complex, multi-host environments** and large-scale applications.  
- It automates the deployment, scaling, service discovery, HA, LB and management of containers across a **cluster of machines**.
- Steps to onboard Kubernetes:
  - Local: minikube, kind, k3d, kubeadm
  - Managed (EKS, AKS, GKE, Openshift) 
