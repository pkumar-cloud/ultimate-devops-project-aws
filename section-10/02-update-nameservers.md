# Update Nameservers for Domain & update ingress resource

## Overview
This guide will help you configure your domain purchased from GoDaddy to use AWS Route 53 for DNS management. Specifically, we will set up the domain (for example - `abhishekveeramalla.shop`) to route traffic to an AWS Application Load Balancer (ALB) using Route 53.

## Steps

### 1. Create a Hosted Zone in Route 53 [Created in the previous lecture]
1. Open the Route 53 console in the AWS Management Console.
2. Click on `Hosted zones` in the navigation pane.
3. Click on `Create hosted zone`.
4. Enter your domain name (example - `abhishekveeramalla.shop`) and select `Public Hosted Zone`.
5. Click on `Create`.

### 2. Create Record Sets in Route 53
1. In the Route 53 console, select your hosted zone for `abhishekveeramalla.shop`.
2. Click on `Create record`.
3. Create an `A` record for `www.abhishekveeramalla.shop`:
    - Name: `www`
    - Type: `A`
    - Alias: `Yes`
    - Alias Target: Select your ALB from the dropdown list.
4. Click on `Create records`.
   <img width="1859" height="773" alt="image" src="https://github.com/user-attachments/assets/f1a262d3-fd8e-4b8d-996d-ec7410d7832c" />

### 3. Update Nameservers in GoDaddy
- Copy the name server details from route 53 and update in GoDaddy so that the ownership of your domain will be managed by route 53.
1. Log in to your GoDaddy account.
2. Navigate to the `My Products` page.
3. Find your domain, example - `abhishekveeramalla.shop` and click on `DNS` or `Manage DNS`.
4. Under `Nameservers`, click on `Change`.
5. Select `Enter my own nameservers (advanced)`.
6. Enter the nameservers provided by AWS Route 53. These can be found in the Route 53 console under your hosted zone details.
7. Save the changes.
   <img width="1304" height="781" alt="image" src="https://github.com/user-attachments/assets/bbda955a-1a6e-442c-b8d2-0bc2d2d3a4bc" />

### 4. Update ingress artifact
```
cd ultimate-devops-project-demo/kubernetes/frontendproxy OR cd ultimate-devops-project-aws/section-9/k8s-manifests/frontendproxy
vim ingress.yaml and update host: example.com #change to your domain: www.<DomainName>
kubectl apply -f ingress.yaml

```
- verify in ALB controller log if new domain name is processed.
```
kubectl logs <ALB-pod-name> -n kube-system #search for your domain name
```

### 5. Verify the Setup [can TAKES UP TO 2 hours to 48 hours]
1. Open a web browser and navigate to `www.abhishekveeramalla.shop`.
2. Ensure that the traffic is routed to your AWS ALB and the website loads correctly.
3. Truoubleshoot:
   - nslookup <www.YourDomainName> #since Route53 alias is updated with www
   - https://www.whatsmydns.net
   - nslookup <ELB-FQDN-FromAWSConsole> #check if it is resolving to IP from above website list
   - Go to ELB -> Listeners and Rules
     <img width="1518" height="664" alt="image" src="https://github.com/user-attachments/assets/87d2852e-3da4-4ded-8ade-534b59d7d4f8" />
   - curl --resolve abhishekveeramalla.shop:80:35.82.250.102 abhishekveeramalla.shop
     - resolving domain to one of the IP from website list. This will be resolved when your ISP have updated its DNS cache.
     - Copy the HTML and render through w3schools


