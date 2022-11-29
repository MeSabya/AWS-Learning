# AWS Lambda Invocation Types

AWS Lambda has 3 Invocation Types;

1. Lambda Synchronous Invocation
2. Lambda Asynchronous Invocation
3. Lambda Event Source Mapping with Polling Invocation


You can all invocation types in one image.

- Synchronous invocation is trigger by push model and execute immediately and wait response. we can say RequestResponse model.
- Asynchronous invocation is trigger by event model and executes asynchronous don’t wait immediate response.
- Event Source Mapping invocation is triggered by poll-based. That means lambda function receives multiple items.

### Lambda Synchronous Invocation
In this communication type, lambda functions execute immediately when you perform the Lambda Invoke by API call.
So when we perform a Lambda invoke an API call, we wait for the function to process the function and return back to response.

A common scenario for synchronous invocation is the API Gateway + Lambda integration:

There are many AWS services that can trigger lambda function synchronously.
Here are some of them:

- ELB (Application Load Balancer)
- Amazon Cognito
- Amazon Lex
- Amazon Alexa
- Amazon API Gateway
- Amazon CloudFront (Lambda@Edge)
- Amazon Kinesis Data Firehose

### Lambda Asynchronous Invocation
In this communication type, Lambda functions works with events and invoke by events and not respond immediately.

Basically we can invoke a lambda function asynchronously, after that Lambda sends the event to a internal queue and returns a success response without any additional information. After that a separate process reads events from the queue and runs our lambda function.

S3 + Lambda + DynamoDB
A common scenario for Asynchronous invocation is the S3 / SNS + Lambda + DynamoDB. You can see in the image of S3 / SNS + Lambda + DynamoDB.





