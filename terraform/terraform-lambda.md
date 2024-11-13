# Creating and Deploying a Lambda using Terraform

Writing your first Terraform to create an AWS Lambda Function requires a few steps:

1. Understand HashiCorp Language (HCL) Syntax
2. Create a Terraform file (`.tf` extension)
3. Write or have a Lambda function code ready to deploy (functions can be written in many languages, but we'll use Python for this example)
4. Download the AWS provider (this happens when you run `terraform init`)
5. Finish by running the remaining terraform commands to validate, plan, and deploy the Lambda Function.

## 1. Understanding HashiCorp (HCL) Syntax

Thankfully, HCL is easy to learn. The basics are language keywords, curly braces, and key/value pairs.

Here's a basic block of HCL to show those three elements in action:
```
provider "aws" {
  region = "us-east-1"
  profile = "dr-java"
}
```

See? Not so bad. 

You can dig more into the basics of the syntax here: https://developer.hashicorp.com/terraform/language/syntax/configuration

If you get the syntax wrong, `terraform validate` will fail and let you know where to look. You're not going to break anything, so just write it!

## 2. Creating a Terraform file

Terraform files end with the `.tf` extension. You can name them whatever you want - when you run your Terraform commands in a folder containing `.tf` files, Terrafrom will detect those and start making sense of them. 
The naming convention for the first Terraform file is `main.tf`. But name it something else, I dare you. Won't change anything. (Later on when we create more resources, we will be creating other `.tf` files with other names that make more sense for what that file actual contains)

Use your IDE of choice (Visual Studio Code works great) and create a new file called `main.tf`. Just make sure it has that `.tf` extension.

Before writing this file you will be

## 3. Lambda Function Code

You should have already taken the Cloud Foundations course and know what an AWS Lambda Function is, but you may not know how to write one.

AWS Lambda Functions at their most basic level have at least a single function to serve as the entry point for the function. The definition of that function depends on the language you choose (AWS Lambda supports several).
For simplicity, we'll use Python.

Create a folder in your project for this code. Create a new Python file named `index.py` (or whatever, just remember what you called it for later). Inside the file write this basic function:

```
def lambda_handler(event, context):
   message = 'Hello {} !'.format(event['name'])
   return {
       'message' : message
   }
```

This function has the ability to accept a name in JSON, and spit back out a custom message. Cool. In the future we'll develop code to actually do stuff.

## 4. Download the AWS Provider

## 5. Testing and Deploying your AWS Lambda Function


