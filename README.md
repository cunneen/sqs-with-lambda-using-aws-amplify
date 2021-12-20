# Implementing SQS Fifo Queue with lambda in AWS Amplify using Cloudformation.

This little tutorial comprises of me implementing an SQS fifo queue in Amplify using cloudformation. 


# Why This tutorial 
SQS is not directly generated by the amplify cli. e.g we can add a lambda using command
`amplify add function` 

But to add SQS, we **do not have** a command like `amplify add queue` etc.

There are multiple ways to add other resouces not supported by CLI as Custom resources. 
Amplify provides two major methods to integrate a custom resouce in our amplify app. 
1. [Use CDK to add custom AWS resources](https://docs.amplify.aws/cli/custom/cdk/)
2. [Use CloudFormation to add custom AWS resources](https://docs.amplify.aws/cli/custom/cloudformation/)

In the first one, you can write your custom resource as simple as in Javascript which on `cdk synth` will convert to cloudformation. 
In the second, you simply provide a cloudformation which it deploys on amplify push.

Both of these methods are absolutely great. However, In my recent project, I was able to deploy SQS with lambda using amplify folder structure and cloudformation without making a seperate folder for custom resources (like in the above methods).

Didn't find much of it online, so just sharing it here for anyone's learning. 

First we need to have a basic amplify backend initialized.  
In order to do so, complete all steps on [Prerequisites](https://docs.amplify.aws/start/getting-started/installation/q/integration/angular/) and [Set up fullstack project](https://docs.amplify.aws/start/getting-started/setup/q/integration/angular/) to have an empty amplify backend initialized. 

Now, we can start by adding a lambda function which will be used to poll from out fifo queue. 
You can add lambda by 
`amplify add function`

![add function](/assets/images/1.png)
This will create an AWS lambda function that will be used to process messages from the queue. 

Now we can see a `function handleOrder` is added into `amplify/backend` folder
![add function](/assets/images/after-lambda.png)

This is present locally, so we need to `amplify push` it so that this lambda is created on the cloud.
![push function](/assets/images/push-lambda.png)

After `push`, you can now go to aws console and check it. (make sure to select your region when viewing since lambda is region based service and it'll be only present in your region)


This `backend` folder containes all resources. So, if we were to add another (custom) resource, we need to create a folder inside it. 

