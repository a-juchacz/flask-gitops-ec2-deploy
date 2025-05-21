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
