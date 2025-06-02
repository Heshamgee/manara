
![Untitled Diagram drawio(2)](https://github.com/user-attachments/assets/0e0a2dc0-5ffc-4c8e-9306-43122b611e15)



AWS cloud-based architecture designed for a scalable, serverless web application

**Project Overview:**
This document describes the components and data flow of an AWS Cloud-based architecture for a scalable, serverless web application with integrated storage, search, cost tracking, and container-based discovery services.


### Web UI Component

1. **Amazon CloudFront**: Delivers the frontend content to users globally with low latency.
2. **Amazon S3 (WebUIBucket)**: Hosts the static frontend assets (HTML, CSS, JS).
3. **AWS WAF**: Protects the application by filtering and monitoring HTTP requests.
4. **AWS AppSync**: Provides GraphQL API for interaction between frontend and backend services.
5. **Amazon Cognito**: Manages user authentication and access control.
6. **AWS Lambda (Settings function)**: Handles frontend settings logic.

---

### Storage Management Component

7. **AWS Amplify**: Provides integration and management for the frontend and hosting workflow.

   * Connected to **Amazon S3 (AmplifyStorageBucket)** for storage needs.

---

### Data Component (Private Subnet)

8. **AWS Lambda (Gremlin Resolver)**: Queries data from Amazon Neptune using the Gremlin query language.

   * **Amazon Neptune**: Graph database service.
9. **AWS Lambda (Search Resolver)**: Queries data from OpenSearch.

   * **Amazon OpenSearch Service**: Provides full-text search and analytics capabilities.

---

### Cost Component

10. **AWS Lambda (Cost function)**: Executes logic to retrieve and process cost data.
11. **Amazon Athena**: Queries CUR (Cost and Usage Reports) stored in S3.
12. **AWS CUR (Cost & Usage Report)**: Delivered to an **S3 Bucket (CURBucket)**.
13. **Amazon S3 (AthenaResultsBucket)**: Stores results of Athena queries.

---

### Image Deployment Component

14. **Amazon S3 (DiscoveryBucket)**: Stores source artifacts or Dockerfile for image creation.
15. **AWS CodeBuild**: Builds container images using the source artifacts.

* Pushes the image to **Amazon Elastic Container Registry (ECR)**.

---

### Discovery Component

16. **Amazon ECS (Elastic Container Service)**: Runs containers managed by AWS Fargate.
17. **AWS Fargate**: Serverless compute engine that runs containerized workloads.

---

### Integration and Management

18. **AWS SDK**: Enables programmatic interaction with AWS services from within the application.
19. **AWS Config**: Tracks and audits AWS resource configurations.

---

### Summary

This architecture leverages multiple AWS services to provide a scalable, secure, and highly available web application. Key features include:

* CDN delivery with CloudFront
* GraphQL API with AppSync
* Secure authentication with Cognito
* Serverless computing with Lambda and Fargate
* Data storage, search, and analytics with S3, Neptune, OpenSearch, and Athena
* Continuous cost tracking using CUR and Athena
* Containerized deployment pipeline with CodeBuild, ECR, and ECS

---


