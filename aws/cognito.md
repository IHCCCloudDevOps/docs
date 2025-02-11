# Amazon Cognito

Amazon Cognito is a tool to handle user authentication and authorization on your website. You can use it to register new users, either through email or also through common login providers (Google accounts, Facebook, etc), handle user sign-ins and what those users are allowed to access on your website.

By using AWS Cognito you are tapping into a secure solution for user management that you do not need to worry about managing yourself. 

## Setting up Amazon Cognito with Amplify

[Follow this guide in the docs to setup `Amplify Auth` which uses `Amazon Cognito` behind the scenes](https://docs.amplify.aws/nextjs/build-a-backend/auth/set-up-auth/)

Basic steps:
1. Install Amplify CLI if you haven't already: `npm install -g @aws-amplify/cli`
2. [Make sure you have run `amplify init` in your project if you haven't already](https://docs.amplify.aws/nextjs/start/manual-installation/)
3. Create a `amplify/auth/resource.ts` file and add the basic auth (with email, as an example but you can choose other login options. See docs for more detail)
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
4. run `npx ampx sandbox` (this requires you to have fresh keys in your aws config file)
5. Now you can use `Authenticator` from `@aws-amplify` package to wrap components in conditional authentication against the server. [Read more here:](https://docs.amplify.aws/nextjs/build-a-backend/auth/connect-your-frontend/using-the-authenticator/)

```js
import { Authenticator } from "@aws-amplify/ui-react";

...

<Authenticator >
      {({ signOut, user }) => (
         // JSX inside this callback function only displays when user is authenticated. Otherwise, it displays the built-in sign-in interface
          <div>
              <h1>Welcome {user?.username}</h1>
              <button><Link href={'/post'}>Make a new post</Link></button>
              <button onClick={signOut}>Sign out</button>
          </div>
      )}
</Authenticator>
```
5. To create a sign-up page (registration) use the `signUp` function and send the required form data to the function. This is all stored on AWS side securely, do you don't need to worry about the management and cannot see users passwords. Read more here: https://docs.amplify.aws/nextjs/build-a-backend/auth/connect-your-frontend/sign-up/
6. Continue to use the `@aws-amplify/auth` package to build out user sign-up and sign-in, and block out features until a user is signed in.
