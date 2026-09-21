# **Docker Init - Simple way of writing Dockerfiles**  
- Magically writes Dockerfile. Comes with **Docker Desktop**.
```
cd src/shipping
docker init
```  

# **Push the Container Images to Registry** 
- docker.io, quay.io, ECR, ACR, GHCR
```
docker login <registry> #Authenticate with container registry
docker push <registry>/<user>/<repository>:<Image-tag>
 - docker push docker.io/pndrns/adservice:v1 OR docker push pndrns/adservice:v1

```

