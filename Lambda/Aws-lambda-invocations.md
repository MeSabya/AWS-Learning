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

Here is a list of services that invoke Lambda functions asynchronously:

S3
EventBridge
SNS
SES
CloudFormation
CloudWatch Logs
CloudWatch Events
CodeCommit
Pool Based Invokes

### Lambda Event Source Mapping with Polling Invocation
Pool-Based invocation model allows us to integrate with AWS Stream and Queue based services. These services don’t invoke Lambda function directly. Lambda will poll from the AWS SQS or Kinesis streams, retrieve records, and invoke functions.
AWS Lambda Event Source Mapping manages the poller and performs Synchronous invokes of our function.

SQS + Lambda
A common scenario for Event Source Mapping with Polling Invocation is the SQS + Lambda. You can see in the image of SQS + Lambda

👉 ***Please follow the below reference as images are not captured here.***

## Reference:
https://medium.com/aws-serverless-microservices-with-patterns-best/aws-lambda-invocation-types-e279ef136347

https://awstip.com/lambda-s3-event-notification-s3-lambda-sns-447093c42c75


