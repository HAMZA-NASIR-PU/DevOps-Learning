# AWS DevOps Learning

## **AWS Roles in Simple Terms**  

An **AWS Role** is like a temporary ID card that gives permissions to a person or a service to access AWS resources.  

### **Example Scenario:**  
Imagine you work in a company, and you need access to a secure room. Instead of giving you a permanent key (which is risky), the company gives you a temporary **visitor badge** that allows you to enter the room only for a limited time.  

Similarly, AWS **roles** provide temporary permissions to users, applications, or services to perform specific actions in AWS without using long-term credentials (like passwords or access keys).  

### **Key Points:**  
✅ **Roles do not belong to a single user** – Unlike IAM users, roles can be assumed by different users, services, or applications.  
✅ **Roles provide temporary access** – This improves security because credentials expire automatically.  
✅ **Roles are used for cross-account or cross-service access** – For example, an EC2 instance can assume a role to access an S3 bucket.  

### **Where AWS Roles are Used?**  
- **EC2 accessing S3** → Instead of storing access keys in the instance, the instance assumes a role with permissions to read/write S3.  
- **Lambda accessing DynamoDB** → The Lambda function assumes a role that allows it to read/write data in DynamoDB.  
- **Cross-account access** → A user in one AWS account can assume a role in another account to perform tasks without needing a new IAM user.  

### **Conclusion**  
AWS Roles help keep AWS environments **secure and flexible** by granting temporary permissions only when needed. Instead of using permanent passwords or keys, services and users can "borrow" permissions using roles. 🚀

- Best article => https://awsfundamentals.com/blog/aws-iam-roles-terms-concepts-and-examples

## **Why Does AWS Lambda Automatically Create a Role?**  

When you create an AWS **Lambda function**, AWS automatically creates an **IAM Role** for the function if you don't specify one. This happens because Lambda needs **permissions** to interact with other AWS services on your behalf.  

### **Why Is This Necessary?**  
A Lambda function often needs to:  
✅ **Write logs to Amazon CloudWatch** 📜 (for debugging and monitoring).  
✅ **Access S3, DynamoDB, or other AWS services** 🛠 (if your function interacts with them).  
✅ **Use other AWS resources** (like SNS, SQS, or Secrets Manager).  

Instead of requiring you to manually set up permissions, AWS creates a **default execution role** for Lambda.  

### **What Does the Default Role Contain?**  
- It typically includes **basic permissions**, such as:  
  - `AWSLambdaBasicExecutionRole`: Allows Lambda to write logs to CloudWatch.  
  - More permissions can be added if your function needs access to other AWS services.  

### **Where Can You Find or Modify This Role?**  
You can check and update the Lambda role by:  
1. Going to **AWS IAM Console** → **Roles**.  
2. Looking for a role named **"AWSLambdaServiceRole-<FunctionName>"**.  
3. Editing its **permissions** if your function needs more access.  

### **Can You Use a Custom Role?**  
Yes! When creating a Lambda function, you can:  
- **Choose an existing IAM role** that already has the required permissions.  
- **Manually create a custom role** and attach it to your function.  

### **Conclusion**  
AWS **automatically** creates a role to make Lambda functional out of the box, ensuring it can log events and interact with AWS securely. If your function needs extra permissions, you must **modify or replace** the role accordingly. 🚀

## **Calling a Simple Lambda Function using AWS CLI**

```javascript
console.log('Loading function');

export const handler = async (event, context) => {
    //console.log('Received event:', JSON.stringify(event, null, 2));
    console.log('value1 =', event.key1);
    console.log('value2 =', event.key2);
    console.log('value3 =', event.key3);
    return {key1: event.key1, key2: event.key2, key3: event.key3};  // Echo back the first key value
    // throw new Error('Something went wrong');
};
```

AWS CLI command is:
`aws lambda invoke / 
--function-name test-function / 
--cli-binary-format raw-in-base64-out / 
--payload '{"key1": "a", "key2": "b", "key3": "c"}' response.json`

Developers Guide of AWS Lambda => https://docs.aws.amazon.com/lambda/latest/dg/welcome.html

## Understanding the Different Ways to Invoke Lambda Functions

https://aws.amazon.com/blogs/architecture/understanding-the-different-ways-to-invoke-lambda-functions/

## AWS Lambda Function URLs: Built-in HTTP endpoints

https://docs.aws.amazon.com/whitepapers/latest/microservices-on-aws/microservices-on-serverless-technologies.html

https://docs.aws.amazon.com/pdfs/whitepapers/latest/microservices-on-aws/microservices-on-aws.pdf
