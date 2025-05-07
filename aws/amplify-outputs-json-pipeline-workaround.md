# AWS Amplify amplify_outputs.json in Pipeline Workaround

## Problem
AWS Amplify requires a file called `amplify_outputs.json` that contains information about the amplify environment. This file can be generated locally using `ampx sandbox` (assuming you have configured your AWS profile locally to make that connection).
The `amplify_outputs.json` is then linked inside you application when using features like their `<Authenticator>` component. Because `amplify_outputs.json` contains potentially sensative information, it is not recommended to push to source control and when an Amplify project is first setup, a line is added to your `.gitignore` to ignore the file.

The problem occurs when trying to run `npm run build` in a non-Amplify CI/CD pipeline. Because `amplify_outputs.json` is linked in the code but not there, you will get a build error. 

The Amplify Docs now include a section about [setting up your own custom pipelines](https://docs.amplify.aws/react/deploy-and-host/fullstack-branching/custom-pipelines/). This involves making the switch from using their pipeline for deployment, to handling that on your own.

I wanted a hybrid approach where I could add custom `GitHub Actions` jobs on my side while also taking advantage of the nicities that come from AWS Amplify's deployment pipeline. 

## Solution

If you just need a build and tests to run that do not require Amplify's backend features actually functioning, then all you need is a blank `amplify_outputs.json` file to be created in the pipeline temporarily for the build to pass.

For that, I added this simple section to my `GitHub Action`:

```yml
# create a dummy json file just to pass tests
- name: Create dummy amplify_outputs file
  run: echo {} > amplify_outputs.json
```

In my case, this allowed us to run `Cypress` UI testing in our `GitHub Action` pipeline and I'll share an example of the whole action below. But this can also be used to allow the project to build for any use case (as long as you don't need the backend actually functioning).

## Sample Cypress GitHub action

```yml
name: Run Tests

on: push
            
jobs: 
    run_tests: 
        name: Run tests
        runs-on: ubuntu-latest
        steps:
            - name: Checkout
              uses: actions/checkout@v4
            # Install npm dependencies, cache them correctly
            - name: Install npm packages
              run: npm install
            # create a dummy json file just to pass tests
            - name: Create dummy amplify_outputs file
              run: echo {} > amplify_outputs.json
            # and run all Cypress tests
            - name: Cypress run
              uses: cypress-io/github-action@v6
              with:
                component: true
                build: npm run build
                start: npm start
```
