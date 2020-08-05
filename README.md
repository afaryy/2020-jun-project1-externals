2020-jun-project1-externals

## Wordpress VPC deploying with Terraform

1. Configure AWS CLI Access Credentials.
Terraform requires that AWS CLI has administrative access to your aws account. Download your access keys and follow the below steps:

```
aws configure
```

2. Clone the github repo "2020-jun-project1-externals". Create a `terraform.tfvars` file as needed.
```
cp terraform.example.tfvars terraform.tfvars
vim terraform.tfvars
```

3. Terraform Initialise. This command is used to initialize a working directory containing Terraform configuration files.This is the first command to start with.  Init will create a hidden directory ".terraform" and download plugins as needed by the configuration.

```
terraform init
```

4. Terraform plan. Run this command to view te execution plan for your configuration. The execution plan specifies what actions Terraform will take to achieve the desired state defined in the configuration, and the order in which the actions occur.

```
terraform plan
```

5. Terraform apply. In the same directory as the main.tf file you created, run the terraform apply command to apply your configuration.After confirming your execution plan as yes, Terraform will create your resource group

```
terraform apply
```
Note there docker commands related to building and uploading the image to ECR.  Terraform apply will have dependencies on these.  See these instructions [below](#docker-commands-to-upload-image-to-ecr).

6. Terraform destroy. Infrastructure managed by Terraform will be destroyed. This will ask for confirmation before destroying.

```
terraform destroy

```

Solution Diagram :

![Wordpress solution diagram02](https://user-images.githubusercontent.com/38310128/88801373-f5876680-d1ec-11ea-8fd1-37cac55a5c9e.jpg)


### Docker commands to upload image to ECR
```
Execute terraform apply before running the below commands

Run below commands to push new word press images to ECR repostiry

ECR_URL=$(aws ecr describe-repositories --region ap-southeast-2 --repository-names wordpress --query 'repositories[].repositoryUri' --output text)

docker tag wordpress:latest "$ECR_URL":latest
docker push "$ECR_URL":latest

Trigger ECS update service to use new image by ECS task
aws ecs update-service --cluster 2020-jun-project1-externals --service 2020-jun-project1-externals --force-new-deployment
````

### Make fille 
````
Run below commands in the root directory create aws resource and docker images

make all

Run below command to destroy using terraform

make destroy
````