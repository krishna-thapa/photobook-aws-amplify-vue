# photobook


## Requirements:
1. Node.js
2. Npm
3. Git
4. Vue (`npm install -g @vue/cli`)
5. AWS Amplify (`npm install -g @aws-amplify/cli`)

## Commands to build the project
1. Create a project (`vue create photobook`)
  - Vue 2.x
  - Dependencies included: Router, Vuex, CSS Pre-processors
  - Tailwind (`vue add tailwind`)
  - Uid (`npm install uuid`)
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
6. Add Auth 
  - `amplify add auth`: Use AWS Cognito service
  - Use simple username for this project
  - `amplify status`: To see the resources status
  - `amplify push`: build all your local backend resources and provision it in the cloud
7. Go through Authentication UI provided by AWS Amplify
  - https://docs.amplify.aws/ui/auth/authenticator/q/framework/vue#usage

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