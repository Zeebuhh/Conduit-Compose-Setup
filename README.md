# Conduit-Compose-Setup

## Table of Contents

- [Description](#description)
- [Project Structure](#project-structure)
- [Quickstart](#quickstart)
- [Usage](#usage)
- [Deployment](#deployment)
- [Troubleshooting](#troubleshooting)

## Description

This repository demonstrates how to set up a full-stack Conduit application using Docker Compose. It consists of two main components:

- **Frontend:** An Angular application served via Nginx.
- **Backend:** A Django-based REST API.

The repository provides all necessary configuration files and scripts to streamline the setup, deployment, and maintenance of the application. Its purpose is to help developers quickly bootstrap their environment and customize it to meet their project requirements.

## Project Structure

- **`.gitignore`**: Ensures only relevant files are committed.
- **`.dockerignore`**: Prevents unnecessary files from being included in Docker images.
- **`.env`**: Stores configuration variables for Docker services.
- **`docker-compose.yaml`**: Defines services, ports, and volumes for the application.
- **`entrypoint.sh`**: Runs migrations and creates a superuser at container startup.

## Quickstart

### Prerequisites

- [Docker](https://docs.docker.com/get-docker/) installed.
- [Docker Compose](https://docs.docker.com/compose/install/) installed.
- Git installed.

### Steps

1. **Clone the repository:**
   ```bash
   git clone https://github.com/Zeebuhh/Conduit-Compose-Setup.git
   cd conduit-compose-setup
   ```
2. **Add the frontend and backend repositories as submodules:**
   ```bash
   git submodule add https://github.com/Zeebuhh/conduit-frontend.git
   git submodule add https://github.com/Zeebuhh/conduit-backend.git
   ```
3. **Ensure required configuration files are in place:**
   - `.env` for environment variables. For instance: [example.env](./example.env). To use the example.env use `cp example.env .env` to rename it.
   - `.gitignore` to exclude unnecessary files.
   - `.dockerignore` to ignore unneeded files during image builds.
4. **Build and start the application:**
   ```bash
   docker-compose up --build
   ```

## Usage

### Configuration Details

- **Environment Variables (`.env`):**  
  Modify this file to set or change configuration variables such as port numbers, database credentials, or other environment-specific parameters.
- **Docker Compose File (`docker-compose.yaml`):**  
  This file defines two primary services:

  - `conduit-frontend`: Serves the Angular application.
  - `conduit-backend`: Runs the Django REST API.  
    Customize port mappings, volume mounts, and service dependencies by editing this file to fit your specific needs.

- **Dockerfiles:**

  - **Frontend Dockerfile:**  
    [Frontend-Dockerfile](./conduit-frontend/Dockerfile)
  - **Backend Dockerfile:**  
    [Backend-Dockerfile](./conduit-backend/Dockerfile)

- **Entry Point Script (`entrypoint.sh`):**

  - [Entrypoint-script](./conduit-backend/entrypoint.sh)

- **Backend Settings:**  
  Update Django settings (e.g., adjusting `ALLOWED_HOSTS`) to reflect your development or production environment.

### Customization Options

- **Modifying Ports and Volumes:**  
  To change the default ports or persist data differently, adjust the `ports` and `volumes` sections in the `docker-compose.yaml` file.
- **Changing Application Behavior:**  
  Both the frontend and backend components are managed as submodules. Modify the source code in these submodules as needed, then rebuild the images using:
  ```bash
  docker-compose up --build
  ```
- **Adding Additional Services:**  
  If you need to add more services (e.g., a database or caching layer), update the `docker-compose.yaml` and add the necessary configuration in the `.env` file.

## Deployment

### Overview

The deployment process is automated using GitHub Actions. When changes are pushed to the `Zeebuhh-patch-1` branch, the workflow updates the application on a remote server via SSH.

### Prerequisites

- A server with SSH access where Docker and Docker Compose are installed.
- The following GitHub Secrets must be configured:
  - `SSH_HOST`: The server’s IP address or domain.
  - `SSH_USER`: The SSH username.
  - `SSH_PRIVATE_KEY`: The private SSH key for authentication.
  - `SSH_PORT` (optional, by default it's 22 for SSH)

### Workflow Steps

1. **Triggered on push to `Zeebuhh-patch-1`.**
2. **Checks out the repository.**
3. **Establishes an SSH connection to the server.**
4. **Clones the repository if it does not exist or pulls updates.**
5. **Runs `docker-compose down` to stop existing containers.**
6. **Rebuilds and restarts containers with `docker-compose up -d --build`.**

### Modifications

- **Branch Configuration:** Change the branch in the workflow file if a different branch should trigger the deployment.
- **Additional Services:** Update the `docker-compose.yaml` file to include new services if needed.
- **Post-Deployment Steps:** If additional setup is required after deployment, extend the SSH script accordingly.

## Troubleshooting

Common commands to diagnose and resolve issues:

- **View logs:**
  ```bash
  docker-compose logs
  ```
- **Rebuild containers:**
  ```bash
  docker-compose up --build
  ```
- **Remove stopped containers and volumes:**
  ```bash
  docker-compose down -v
  ```
