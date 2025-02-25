# Conduit-Compose-Setup

## Table of Contents

- [Description](#description)
- [Project Structure](#project-structure)
- [Quickstart](#quickstart)
- [Usage](#usage)
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
   #bash
   git clone https://github.com/Zeebuhh/Conduit-Compose-Setup.git
   cd conduit-compose-setup
   ```
2. **Add the frontend and backend repositories as submodules:**
   ```bash
   #bash
   git submodule add https://github.com/Zeebuhh/conduit-frontend.git # conduit-frontend
   git submodule add https://github.com/Zeebuhh/conduit-backend.git # conduit-backend
   ```
3. **Ensure required configuration files are in place:**
   - `.env` for environment variables. For instance: [example.env](./example.env).
   - `.gitignore` to exclude unnecessary files.
   - `.dockerignore` to ignore unneeded files during image builds.
4. **Build and start the application:**
   ```bash
   #bash
   docker-compose up --build
   ```

## Usage

This section details the configuration and customization options available in the repository.

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
  #bash
  docker-compose up --build
  ```
- **Adding Additional Services:**  
  If you need to add more services (e.g., a database or caching layer), update the `docker-compose.yaml` and add the necessary configuration in the `.env` file.

## Troubleshooting

Common commands to diagnose and resolve issues:

- **View logs:**
  ```bash
  #bash
  docker-compose logs
  ```
- **Rebuild containers:**
  ```bash
  #bash
  docker-compose up --build
  ```
- **Remove stopped containers and volumes:**
  ```bash
  #bash
  docker-compose down -v
  ```
