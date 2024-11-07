# Terraform 101

Terraform works as a go-between for your code (written in Hashi Corp Language, or HCL) and a cloud provider (in our case AWS, but Terraform supports several).

In practice, this means you can type Terraform commands in your console to verify HCL code and to communicate with your cloud provider.
Here are some of the basic Terraform commands and what they do.

## Terraform Commands
`terraform init`

Initializes terraform in the current directory. This sets up terraform by downloading any necessary `providers`.

`terraform format` or `terraform fmt`

Formats the HCL into standardized formating. This is optional, but can be nice to do after adding new changes.

`terraform validate`

Validates any syntax errors in the HCL. Should be ran before attempting to `plan` or `apply`.

`terraform plan`

Takes the HCL and compiles a list of what would be created, altered, or destroyed with the current code.
This is actually pretty cool because it will also communicate with the cloud platform (if this is configured in the current environment)
and check the current resources in the cloud with the proposed HCL to check for those discrepancies.

`terraform apply`

This will take the current plan (after running `terraform plan`) and attempt to deploy it to the chosen cloud provider. 
This requires that link be made in the current environment - the link being credentials for the cloud platform set in environment variables. 
NEVER set credentials within terraform files or any other files for that sake. That leaves them in plain text and easy for misuse. 

`terraform destroy`

Deletes all the resources in the plan from the cloud provider. Use this if you want to tear everything down (in this class we'll use it a lot so that we don't leave unused resources on AWS costing us money).

### Glossary
`provider`'s are cloud platform specific connector libraries that connect your environment with the cloud platform, and converts the HCL into actual cloud services.
