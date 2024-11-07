# Configuring Terraform with AWS CLI credentials

You can use Terraform by itself to an extent - you can write, format and validate cloud resources without actually speaking to the cloud platform.
However, when you want to actually deploy your infrastructure to the cloud (the whole point) you'll need to configure a connection, and that requires authenticating.

You have two options for this:
1. Set up a role in your cloud provider specific to deploying with terraform (preferred)
2. Use your own development account (only for local, les preferred)

When we start using terraform in our CI/CD pipelines, we'll configure the first option. But for local testing and our initial setup, we'll use the second option.

Good news: if you setup AWS CLI and use `aws configure` to setup sso login, terraform will automatically pick up these credentials. It's magic. (it's not, it looks under your user directory for the `.aws` folder and finds the config and credential files).

If I forget to link the guide here about setting up AWS CLI, please remind me. This is my TODO to do that.
