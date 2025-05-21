# Flask EC2 Hello World

A simple Flask application that returns "Hello from EC2!" when accessed.

## Setup and Running

### Local Development

1. Install dependencies:
```bash
pip install -r requirements.txt
```

2. Run the application:
```bash
python app.py
```

The application will be available at `http://localhost:80`

### Docker

1. Build the Docker image:
```bash
docker build -t flask-ec2-app .
```

2. Run the container:
```bash
docker run -p 80:80 flask-ec2-app
```

The application will be available at `http://localhost:80`

## Continuous Deployment

This project uses GitHub Actions for continuous deployment to EC2. The workflow automatically builds and deploys the application when changes are pushed to the main branch.

### Prerequisites

1. Create an ECR repository named `flask-ec2-app` in your AWS account
2. Create an IAM role for GitHub Actions with the following permissions:
   - `AmazonECR-FullAccess`
   - `AmazonEC2ContainerRegistryFullAccess`
3. Configure the EC2 instance with:
   - IAM role that has ECR pull permissions
   - AWS CLI installed
   - Docker installed

### Required Secrets

The following secrets need to be configured in your GitHub repository:

- `AWS_ACCOUNT_ID`: Your AWS account ID
- `AWS_ROLE_ARN`: The ARN of the IAM role for GitHub Actions
- `EC2_HOST`: The public IP or hostname of your EC2 instance
- `EC2_USERNAME`: The username for SSH access (usually 'ec2-user' or 'ubuntu')
- `EC2_SSH_KEY`: The private SSH key for accessing the EC2 instance

### Workflow Steps

1. Authenticates with AWS using OIDC
2. Logs into Amazon ECR
3. Builds the Docker image
4. Pushes the image to ECR
5. SSH into the EC2 instance
6. Logs into ECR on the EC2 instance
7. Stops and removes any existing container
8. Pulls the latest image
9. Runs the new container
