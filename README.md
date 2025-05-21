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

### Required Secrets

The following secrets need to be configured in your GitHub repository:

- `DOCKER_USERNAME`: Your Docker Hub username
- `DOCKER_PASSWORD`: Your Docker Hub password or access token
- `EC2_HOST`: The public IP or hostname of your EC2 instance
- `EC2_USERNAME`: The username for SSH access (usually 'ec2-user' or 'ubuntu')
- `EC2_SSH_KEY`: The private SSH key for accessing the EC2 instance

### Workflow Steps

1. Builds the Docker image
2. Pushes the image to Docker Hub
3. SSH into the EC2 instance
4. Stops and removes any existing container
5. Pulls the latest image
6. Runs the new container
