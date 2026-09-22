# Kubernetes: LoadBalancer Service Type vs Ingress

In Kubernetes, both LoadBalancer service type and Ingress are used to expose services to external traffic. However, they serve different purposes and have distinct characteristics. This document explains the differences between the two in detail.

## LoadBalancer Service Type

### Overview
- The LoadBalancer service type is a way to expose a service to external traffic by provisioning an external load balancer.
- It is typically used to expose a single service to the internet.

### Characteristics
- **Automatic Provisioning**: When a LoadBalancer service is created, Kubernetes automatically provisions an external load balancer from the cloud provider. No external controller e.g. nginix controller etc.. thus less operations overhead. 
- **Single Service Exposure**: Each LoadBalancer service exposes a single service.
- **Cloud Provider Dependent**: The implementation and features of the LoadBalancer depend on the cloud provider (e.g., AWS, GCP, Azure).
- **Static IP**: It usually provides a static IP address for the service.

### Limitations/Downside
- **Not Declarative**: SVC -> API server -> CCM -> AWS -> LB. Kubernetes automatically provisions an external load balancer from the cloud provider. But this is **HTTP**, if wants to make to HTTPS, needs to be done manually configure at AWS side, thus no track/declaration/control at K8S side.
- **Not Cost effective**: Each LoadBalancer service exposes only a single service.
- **Not Flexible/Tied to CCM**: Tied to Cloud. Can not use 3rd party LB's e.g. F5, nginx, traefik in SVC.
- **No Local support**: as it is tied to CCM, can not support LB type SVC on local setups like minikube, kind etc..

### Use Cases
- Suitable for exposing a single service to the internet.
- Ideal for simple use cases where advanced routing is not required.

## Ingress

### Overview
- Ingress is a Kubernetes resource that manages external access to services within a cluster, typically HTTP and HTTPS.
- It provides more advanced routing capabilities compared to the LoadBalancer service type.

### Characteristics/Pros
- **Declarative**: A yaml file, update LB's configs easily.
- **Flexible**: 3rd party LB's e.g. F5, nginx, traefik are supported, just depends upon the Ingress controller type.
- **Local support**: as it is not tied to CCM, can support local setups like minikube, kind etc.. and create external IP's say using reverse proxy or similar mechanism.
- **Single Entry Point**: It provides a single entry point for multiple services. Can route to multiple services using host-based or path-based routing. Thus **Cost effective**.
- **Advanced Routing**: Ingress can route traffic to multiple services based on hostnames, paths, and other rules.
- **TLS Termination**: Ingress can handle TLS termination, providing secure HTTPS access.
- **Requires Ingress Controller**: An Ingress resource requires an Ingress controller to be deployed in the cluster (e.g., NGINX, Traefik).

### Use Cases
- Suitable for exposing multiple services through a single IP address.
- Ideal for complex routing scenarios, such as path-based or host-based routing.
- Useful for managing SSL/TLS certificates and providing secure access.

## Comparison Table

| Feature                  | LoadBalancer Service Type | Ingress                        |
|--------------------------|---------------------------|-------------------------------|
| Provisioning             | Automatic by cloud provider| Requires Ingress controller   |
| Service Exposure         | Single service            | Multiple services             |
| Routing Capabilities     | Basic                     | Advanced (host/path-based)    |
| TLS Termination          | No                        | Yes                           |
| Cloud Provider Dependency| Yes                       | No                            |
| Use Case                 | Simple, single service    | Complex, multiple services    |

## Conclusion

Both LoadBalancer service type and Ingress are essential tools in Kubernetes for exposing services to external traffic. The choice between them depends on the specific requirements of your application. Use LoadBalancer for simple, single-service exposure and Ingress for more complex scenarios requiring advanced routing and secure access.
