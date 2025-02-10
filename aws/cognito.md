# Amazon Cognito

Amazon Cognito is a tool to handle user authentication and authorization on your website. You can use it to register new users, either through email or also through common login providers (Google accounts, Facebook, etc), handle user sign-ins and what those users are allowed to access on your website.

By using AWS Cognito you are tapping into a secure solution for user management that you do not need to worry about managing yourself. 

## Setting up Amazon Cognito with Amplify

Follow this guide in the docs to setup `Amplify Auth` which uses `Amazon Cognito` behind the scenes: https://docs.amplify.aws/nextjs/build-a-backend/auth/set-up-auth/

Basic steps:
1. Make sure you have run `amplify init` in your project if you haven't already (https://docs.amplify.aws/nextjs/start/manual-installation/)
2. Create a `amplify/auth/resource.ts` file and add the basic auth (with email, as an example but you can choose other login options. See docs for more detail)
   ```js
         import { defineAuth } from "@aws-amplify/backend"
      
      /**
       * Define and configure your auth resource
       * @see https://docs.amplify.aws/gen2/build-a-backend/auth
       */
      export const auth = defineAuth({
        loginWith: {
          email: true,
        },
      })
   ```
3. run `npx ampx sandbox` (this requires you to have fresh keys in your aws config file)
4. 
