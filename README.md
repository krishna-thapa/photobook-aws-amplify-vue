# photobook
**Full Stack Photobook App | Vue, GraphQL, AWS Amplify**
From [Youtube Tutorial](https://www.youtube.com/watch?v=w0p7ywfHesw)

The web app is build and hosted in AWS cloud using AWS Amplify that builds an app backend with auth. User first have to sign up and login to the app for the authentication that is provided by AWS Cognito service. When you successfully sign up the app, you will be sent the verification code in the email. Once the user is in home page, user can run albums and photos model schema using GraphQL service using AWS AppSync with AWS DynamoDB. User can upload and load the uploaded images using storage provided by S3 service from AWS.

## Requirements:
1. [Node.js](https://nodejs.org/en/) with version 11 or higher
2. [Npm](https://www.npmjs.com/)
3. [Git](https://git-scm.com/)
4. [Vue 2.x](https://vuejs.org/) (`npm install -g @vue/cli`)
5. [AWS Amplify](https://aws.amazon.com/amplify/) (`npm install -g @aws-amplify/cli`)

## Commands to build the project
1. Create a project (`vue create photobook`)
  - Dependencies included: Router, [Vuex](https://vuex.vuejs.org/), CSS Pre-processors
  - [Tailwind](https://tailwindcss.com/) (`vue add tailwind`)
  - [Uuid](https://www.npmjs.com/package/uuid) (`npm install uuidv4`)
  - VSCode plugin: Tailwind CSS IntelliSense
2. Set up AWS Amplify 
  - `amplify configure`
  - Login into AWS account and select the region
  - Create a user to use the Amplify service
  - Get the Access Id and Secret access key and copy to the terminal
3. Create Amplify project in AWS Amplify Service
  - `amplify init`: Under the root project
  - Select the project name in Amply service and environment 
  - `npm run build`: For Build command  
  - **Uses the CloudFormation**
  - Creates a amplify folder under root project that has all the configuration for the project
4. Add aws-amplify libraries for the Vue project
  - `npm install aws-amplify @aws-amplify/ui-vue`
5. Add aws-amplify configuration in main.js
  - [Official documentation](https://docs.amplify.aws/start/q/integration/vue)
  ```
  import Amplify from 'aws-amplify'
  import '@aws-amplify/ui-vue'
  import aws_exports from `./aws-exports`

  Amplify.config(aws_exports)
  ```
6. Add Auth using [AWS Cognito](https://aws.amazon.com/cognito/)
  - `amplify add auth`: Use AWS Cognito service
  - Use simple username for this project
  - `amplify status`: To see the resources status
  - `amplify push`: build all your local backend resources and provision it in the cloud
7. Go through Authentication UI provided by AWS Amplify
  - https://docs.amplify.aws/ui/auth/authenticator/q/framework/vue#usage
8. Add [GraphQl](https://aws.amazon.com/graphql/) and [S3 storage](https://aws.amazon.com/s3/)
  - [Guide](https://docs.amplify.aws/lib/storage/getting-started/q/platform/js)
  - Store all the uploaded pictures in S3 bucket
  - There are two ways to add storage with Amplify - manual and automated. Both methods require the `auth` category with Amazon Cognito to also be enabled.
  - `amplify add storage`: Creates a storage in S3 bucket using Cloudformation
  - Make the content for Images, give the resource name and bucket name and make user only the Auth users can have access to perform CRUD operation on the storage
  - `amplify status`: To see the new resources added 
9. Adding Lambda in AWS Amplify
10. Add [AWS AppSync](https://aws.amazon.com/appsync/)
  - [Guide](https://docs.amplify.aws/lib/graphqlapi/getting-started/q/platform/js)
  - AWS AppSync is a fully managed service that makes it easy to develop GraphQL APIs by handling the heavy lifting of securely connecting to data sources like AWS DynamoDB, Lambda, and more. 
  - `amplify add api`: To create a GraphQL API, use the Amplify add command
  - Select `GraphQL` as a service with Amazon Cognito User Pool for default authorization and in advance settings, select `IAM` for additional authorization. FInally choose Single object with fields for a schema template
10. Configure `schema.graphql`
  - Added model and auth to graphql schema type, see more in [documentation](https://docs.aws.amazon.com/appsync/latest/devguide/designing-your-schema.html) 
  - See more details on `@auth`, `@model` and `@connection`
11. Mocking GraphQL API with Playground
  - Check the `amplify status`: Should have three resources: Storage, Api and Auth
  - Run the project: `npm run serve` and sign to your account since mocking graphql requires validate auth
  - Open second terminal and run: `amplify mock api`
  - Open the localhost with port: `20002`
  - It can be also done through AWS AppSync but it will make changes to Production data
  - You can see the query, mutation and subscription that are generated using schema file
  - `amplify push`: To update the new aws services in aws amplify
12. Add Lambda function
  - `amplify add function`: Select the serverless function and give the function name 
  - Select `api` under the access other resources in the project from lambda function
  - Select the operations that you want to permit for api from function, can be CRUD operations
  - Go to sun folder `/amplify/backend/function/AmplifyPhotoProcessor/src`
  - Install axios: `npm install axios aws4 exif-reader`
  - To read GPS library: `npm install --arch=x64 --platform=linux sharp`
12. [AWS Amplify](https://aws.amazon.com/amplify/features/#API) -> AWS Cognito Auth -> AppSync -> AWS DynamoDB -> S3 Storage -> AWS Lambda
  - AWS Amplify is a set of tools and services that can be used together or on their own, to help front-end web and mobile developers build scalable full stack applications, powered by AWS
  - Amplify Auth lets you quickly set up secure authentication flows with a fully-managed user directory. Control what users have access to in your mobile and web apps with Amplify Auth's built-in authorization capabilities. Click options together or use guided commands to configure email and social sign-up/sign-in, forgot password, and multi-factor auth workflows.
  - Make secure HTTP requests to GraphQL and REST endpoints to access, manipulate, and combine data from one or more data sources such Amazon DynamoDB, Amazon Aurora Serverless, and your custom data sources with AWS Lambda. 
  - The AWS Amplify Storage module provides a simple mechanism for managing user content for your app in public, protected or private storage buckets. Leverage cloud scale storage so that you can easily take your application from prototype to production. Powered by Amazon S3.
  - Add a Lambda function to your project which you can use alongside a REST API or as a datasource in your GraphQL API using the @function directive in the Amplify CLI. 

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).


## Knows problems 
- Fix 'TypeError: getProcessedPlugins is not a function' error after updating Tailwind to 2.0: [Solution](https://bubalubs.io/updating-tailwind-to-v2-0/)
- Module not found: Error: Can't resolve '../aws-exports': [Solution](https://stackoverflow.com/questions/60154820/module-not-found-error-cant-resolve-aws-exports-react-native-expo-web)