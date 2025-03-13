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
