# my-flask

A simple Flask application with Docker containerization and CI/CD pipeline.

## Features

- Simple Flask web application with health endpoint
- Docker containerization with security best practices
- GitHub Actions CI/CD pipeline for automatic Docker image building and pushing to Docker Hub
- Multi-stage build optimization and caching

## Local Development

### Prerequisites

- Python 3.11+
- Docker
- Git

### Running Locally

1. Install dependencies:
```bash
pip install -r requirements.txt
```

2. Run the application:
```bash
python app.py
```

The application will be available at `http://localhost:5000`

### Endpoints

- `GET /` - Main application endpoint
- `GET /health` - Health check endpoint

## Docker

### Building the Image

```bash
docker build -t my-flask-app .
```

### Running the Container

```bash
docker run -p 5000:5000 my-flask-app
```

## CI/CD Pipeline

The GitHub Actions workflow automatically:

1. **Builds** the Docker image on every push to main/master branches and tags
2. **Tests** the container by running health checks
3. **Pushes** the image to Docker Hub (when not a pull request)
4. **Tags** images appropriately based on branch/tag/commit

### Required Secrets

To use the Docker Hub integration, add these secrets to your GitHub repository:

- `DOCKER_USERNAME` - Your Docker Hub username
- `DOCKER_PASSWORD` - Your Docker Hub password or access token

### Image Tags

The pipeline creates multiple tags:
- `latest` - Latest build from the default branch
- `<branch-name>` - Branch-specific builds
- `<tag>` - Release tags (for semantic versioning)
- `<branch>-<sha>` - Commit-specific tags

## Security

- Container runs as non-root user
- Minimal attack surface with Python slim base image
- Dependencies installed with SSL verification fallback
- Health checks included for container orchestration