# Cloud Resume

## Project Summary

In this project I developed and deployed a full-stack portfolio website utilizing various AWS services to ensure a secure and scalable solution. The resume website features a JavaScript visitor counter storing data on a DynamoDB database, that is accessed and updated via an API endpoint I made through API-Gateway and AWS Lambda function written in Python. The web assets are stored inside an S3 bucket, which is served via CloudFront distributions with DNS management done through my Route53 hosted zones. 

I initially set up a manual deployment (`resume.satwik.in`), and later created a fully automated Terraform-managed version (`terraformed-resume.satwik.in`) to demonstrate Infrastructure as Code practices. Both deployments share the same frontend codebase but have independent backend infrastructure.

The entire infrastructure is also defined and managed via Terraform for the terraformed version.

View [resume.satwik.in](https://resume.satwik.in) (standard version) or [terraformed-resume.satwik.in](https://terraformed-resume.satwik.in) for the terraformed version

## Technologies and Tools

- **JavaScript**
- **jQuery**
- **AWS S3**
- **AWS CloudFront**
- **AWS Route 53**
- **AWS DynamoDB**
- **AWS API Gateway**
- **AWS Lambda (Python)**
- **AWS CLI**
- **GitHub Actions**
- **Terraform**

## Features

1. **Static Website Hosting with AWS S3:**
   - Deployed the portfolio website on AWS S3 buckets.
   - Configured CloudFront Origin Access Control (OAC) to secure bucket access (bucket is not publicly accessible).
   - Automated file uploads via Terraform for the terraformed version.

2. **Secure Content Delivery with AWS CloudFront:**
   - Set up CloudFront to distribute the content globally with low latency.
   - Configured HTTPS for secure data transmission using ACM certificates.
   - Implemented custom caching policies to improve performance.

3. **Custom Domain Configuration:**
   - Domain registered at Hostinger (`satwik.in`).
   - Configured DNS records in Route 53 to point to CloudFront distributions.
   - Both subdomains (`resume.satwik.in` and `terraformed-resume.satwik.in`) route to their respective CloudFront distributions.

4. **Visitor Counter:**
   - Developed a JavaScript-based visitor counter displayed on the website.
   - Visitor data is stored in DynamoDB.
   - Implemented a RESTful API using AWS API Gateway and Lambda functions to interface with the DynamoDB table.
   - Used the `boto3` library in Python for seamless integration with DynamoDB.
   - Also configured Lambda Function URLs as an alternative access method.

5. **Continuous Integration and Deployment (CI/CD):**
   - Utilized GitHub Actions to automate the deployment process.
   - Configured workflows to automate cache invalidation and deployment to S3.
   - For the terraformed version, the pipeline automatically deploys the entire infrastructure via Terraform on every push.

6. **Security and Best Practices:**
   - Ensured AWS credentials were securely managed and excluded from source control.
   - Implemented CloudFront OAC to prevent direct S3 bucket access.
   - Configured IAM roles with least-privilege policies.
   - Set up proper CORS headers for API endpoints.

## Architecture 

![Architecture Diagram](https://github.com/user-attachments/assets/d0905155-96c3-4cc9-b497-c4ae474c8224)

The project features two parallel deployments:

- **Standard Version (`resume.satwik.in`):** Initially created manually through AWS Console, now uses CI/CD for frontend deployments.
- **Terraformed Version (`terraformed-resume.satwik.in`):** Fully automated Infrastructure as Code deployment using Terraform, with remote state management (S3 + DynamoDB locking).

Both versions use the same frontend codebase but have separate backend infrastructure (DynamoDB tables, Lambda functions, API Gateways).

## Getting Started

### Prerequisites

- AWS Account
- GitHub Account
- Basic knowledge of AWS services, Python, and JavaScript

### Installation and Deployment

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/ssatwik975/resume-site.git
   cd resume-site
   ```

2. **Configure AWS CLI:**
   ```bash
   aws configure
   ```

3. **Set Up S3 Buckets:**
   - Create an S3 bucket for hosting the website.
   - Upload the website files to the S3 bucket.

4. **Set Up CloudFront:**
   - Create a CloudFront distribution pointing to the S3 bucket.
   - Configure HTTPS and caching policies.

5. **Configure Route 53:**
   - Register a custom domain.
   - Set up DNS records to point to the CloudFront distribution.

6. **Deploy Lambda Functions:**
   - Write and deploy Lambda functions using the `boto3` library for DynamoDB integration.
   - Set up API Gateway to expose the Lambda functions as a RESTful API.

7. **Configure CI/CD with GitHub Actions:**
   - Set up workflows in the `.github/workflows` directory.
   - Configure actions to automate deployment and cache invalidation.


### License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgments

- AWS for providing robust and scalable cloud services.
- The open-source community for the libraries and tools utilized in this project.
