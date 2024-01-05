# AWS DIAGRAM OF LINKED

As the developer of `LINKED`, a toll road operator company, I have undertaken the task of migrating our existing on-premise toll management application to `Amazon Web Services (AWS)`. In my role as a `Cloud Solution Architect/Consultant`, I have designed a comprehensive cloud-based solution that incorporates AWS services to effectively capture vehicle plate images and automatically charge driver accounts based on various factors such as vehicle type and distance traveled. This solution enables LINKED to collect fees from drivers using our toll system efficiently.

---

## AWS Architectural Diagram Overview

This architectural diagram illustrates the flow of operations within LINKED's toll management system on AWS:

1. A vehicle passes through the toll, triggering the toll camera to capture images utilizing the [`AWS SDK`](https://aws.amazon.com/sdk-for-javascript/).
2. Captured license plate images are securely stored in the [`Amazon S3`](https://aws.amazon.com/s3/) of LINKED, ensuring data integrity.
3. An [`AWS Lambda`](https://aws.amazon.com/lambda/) function processes the captured image, resizing it and eliminating extraneous details, focusing solely on pertinent information.
4. [`Amazon Rekognition`](https://aws.amazon.com/rekognition/) extracts the license plate number from the resized image.
5. Extracted images are transmitted to the [`Amazon SQS`](https://docs.aws.amazon.com/lambda/latest/dg/with-sqs.html) message queue for streamlined processing.
6. Another Lambda function retrieves messages from the SQS queue, utilizing the license plate number to fetch vehicle specifics from the [`Aurora RDS`](https://aws.amazon.com/rds/aurora/).
7. [`AWS Step Functions`](https://aws.amazon.com/step-functions/) coordinate multiple Lambda functions, managing the transmission of vehicle details and the storage of driver account information within [`AWS DynamoDB`](https://aws.amazon.com/dynamodb/).
8. Within LINKED, a distinct Lambda function harnesses the [`Amazon Location Service`](https://aws.amazon.com/location/) to compute the distance traveled by the vehicle from its origin to its destination based on geographical coordinates.
9. Calculated distances are logged in DynamoDB to update the distance traveled. This Lambda function also processes vehicle type, distance, and license plate number, computing the total toll fee and storing it in DynamoDB.
10. [`AWS CloudFront`](https://aws.amazon.com/cloudfront/) is utilized for webpage deployment, complemented by [`Route 53`](https://aws.amazon.com/route53/) to manage incoming routes. [`AWS WAF (Web Application Firewall)`](https://aws.amazon.com/waf/) fortifies the system with robust firewall protection.
11. [`AWS Cognito`](https://aws.amazon.com/cognito/) seamlessly manages user authentication and authorization protocols.
12. [`Amazon API Gateway`](https://aws.amazon.com/api-gateway/) facilitates communication with the toll management application, creating RESTful APIs for drivers to interact seamlessly within the system.
13. [`IAM policies`](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html) meticulously delineate resource access permissions for different stakeholders.
14. Toll bills are dispatched to users via email using [`Amazon SES`](https://aws.amazon.com/ses/) and Lambda functions.
15. The payment process within LINKED is fully automated.
16. A dedicated Lambda function accesses the toll fee database.
17. AWS Step Functions orchestrate the payment process, updating transaction statuses within the database and resetting toll fees upon successful completion.
18. Upon a successful transaction, an acknowledgment email is dispatched to the user's device via Amazon SES.

---

Feel free to clone this repository and explore the detailed implementation and codebase for LINKED's AWS-based toll management system.

## Installation and Usage

### Prerequisites
- `AWS account` with necessary permissions
- Set up `AWS services` as per the provided architecture diagram
- Set up `draw.io` account

### Instructions
1. Clone this repository.
```bash
git clone https://github.com/A02kash/linked-toll-management.git
```
2. Navigate to the relevant directories for detailed instructions on setting up and deploying specific components.
```bash
https://docs.aws.amazon.com/accounts/latest/reference/manage-acct-creating.html
```
3. Follow the documentation to deploy and manage the toll management system on AWS.

---

