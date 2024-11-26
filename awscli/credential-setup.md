# AWS CLI Credential Setup Instructions

To connect to an AWS account and interact with resources using AWS CLI you must first establish credentials locally.  

1. Sign-in to the AWS apps portal provided to you by your instructor.
2. Select the role associated with this course and select the Access Keys button to see the keys to configure.
3. In your terminal, type the command ‘aws configure’ and fill in the responses with your keys.
4. For default region, choose us-east-1
5. For default output format, choose json 

Running the `aws configure` command and filling it out will create a file called credentials in your `user/.aws directory.` Open this file to verify your credentials. 

## Temporary vs. Long-term Access Keys

Access keys starting with `ASIA....` are temporary access keys. These require an additional line to be added to your credentials file for the session token, like this: 

`aws_session_token=IQrRds.....etc`

Session tokens will need to be updated periodically, so if you have issues authenticating, check these token value and see if it’s out of date. 

If your access key starts with `AKIA...` these are long term access keys, and do not need the session token. 

## Verifying Credentials

You can verify that your credentials were setup correctly by attempting to use an AWS CLI tool that connections with your AWS account.
For example try running: `aws s3 ls` to list all S3 buckets on the account. If it doesn't throw an authentication error, you are good to go!
 
