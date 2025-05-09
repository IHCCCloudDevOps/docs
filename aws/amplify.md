# Deplying an Amplify App

Amplify is an AWS frontend serverless service that allows us to host server-side rendered (SSR) websites that are pay-as-you-go (and very inexpensive).

Rather than pay a set monthly fee for an EC2 instance running a web server, Amplify charges only for build time (every time you make changes to your website and it has to build and deploy a new version) and requests. 
This results in a very affordable website hosting service for low-traffic apps. 

## Setup project for Amplify

We want Amplify Gen 2 (that's the latest). For that, follow these setup instructions for our existing NextJS project - https://docs.amplify.aws/nextjs/start/manual-installation/

This involves running `npm create amplify@latest` in your existing project directory. Let it do it's magic. We will use some of these files later as scaffolding for authentication and backend services.


## Deploying Amplify Resource using Terraform (👎)

The [AWS terraform provider does include an Amplify resource](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/amplify_app), but GitHub actions doesn't seem to play nice with this right now.
We should be able to use the `access_token` parameter to give AWS access, but there are currently issues with this. (see the following error below and Google bugs)
`
Error: creating Amplify App (blippy-social-app): operation error Amplify: CreateApp, https response error StatusCode: 400, RequestID: 0ba70130-9fb6-4c0f-8862-1fc92bf498ce, BadRequestException: There was an issue setting up your repository. Please try again later.({"message":"Not Found","documentation_url":"https://docs.github.com/rest/repos/webhooks#list-repository-webhooks","status":"404"})
`
## Deploy using Amplify Pipeline (👍)

AWS Amplify offers a build pipeline that you can configure from the AWS console and connect to your GitHub repo. When a new push is detected on the configured branch, the code will be pulled, built, and deployed automatically. We will do this until I can get the Terraform/GitHub Actions working.

You can use [this documentation](https://docs.aws.amazon.com/amplify/latest/userguide/setting-up-GitHub-access.html) to get this setup from the AWS console side. 

Basically:
- Go to Amplify in the AWS Console (make sure you are in the same region as your other services will be)
- Click "Create new app"
- Select GitHub as code repository
  - Don't start with a template, you should have already created your NextJS app locally
- Add your repository as the source and pick the main branch as the branch it will build from (and maybe think about in the future not just using the main branch for everything, but only using it for your production ready code)
  - I already did the step on our shared AWS account to authorize our GitHub Organization (IHCCCloudDevOps). As long as your repo is in there, it should populate just fine.
  - If you have your frontend code in a subdirectory and not the root directory of the repo, then check the box for `monobuild` and type the name of that subdirectory.
  - Verify the details are correct on the next page (should auto detect nextJS as framework and `.next` as build directory. Save and Deploy.
  - After deploy is finished, you should be able to hit the provided URL and see your site live! Any pushes to the main branch will kick off another build/deploy on AWS.
