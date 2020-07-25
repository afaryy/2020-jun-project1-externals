2020-jun-project1-externals

## Wordpress VPC deploying with Terraform 

1. Configure AWS CLI Access Credentials.
Terraform requires that AWS CLI has administrative access to your aws account. Download your access keys and follow the below steps:

```
 aws configure

```

2. Clone the github repo "2020-jun-project1-externals" and checkin to the folder. Update terraform.tfvars file with your home IP-address in the following format. 

```
yourhomenetworkip = "x.x.x.x/32"

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
6. Terraform destroy. Infrastructure managed by Terraform will be destroyed. This will ask for confirmation before destroying.

```

terraform destroy

```
