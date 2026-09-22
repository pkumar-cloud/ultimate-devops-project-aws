# Notes:
- create eks-install/modules, eks & vpc #write the reusable code for eks & vpc.
- Each folder contains main.tf (actual code), variables.tf (variables to pass to main.tf), output.tf (directs what to print after execution). In these subfolders main.tf starts directly with "resources" since it is reusabled. 
- Engineer will create "eks-install/main.tf" to call these modules and mention "provider", this is the main program which will consume modules.
```
cd eks-install/backend
- create s3 & dynamodb infra for next steps.
terraform init 
terraform plan
terraform apply
--------
cd eks-install
terraform init  #initializes the remote backend here.
terraform plan #Dry run. state lock is acquired here
terraform apply
terraform destroy

```
