# Conduit-Compose-Setup

This repository demonstrates how to set up a full-stack Conduit application using Docker Compose.

## Overview

The repository includes two main components:

- **Frontend:** An Angular application served via Nginx.
- **Backend:** A Django-based REST API.

Additionally, there are configuration files and scripts that streamline the setup and deployment process, making it easy to start, configure, and maintain the application.

## Project Structure

- **`.gitignore`:** Ensures only relevant files are committed.
- **`.dockerignore`:** Prevents unnecessary files from being included in Docker images.
- **`.env`:** Stores configuration variables for Docker services.
- **`docker-compose.yaml`:** Defines services, ports, and volumes for the application.
- **`entrypoint.sh`:** Runs migrations and creates a superuser at container startup.

## Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/your-repo/conduit-compose-setup.git
   cd conduit-compose-setup
   ```
2. Add the frontend and backend repositories as submodules:

   ```bash
   git submodule add <frontend-repo-url> conduit-frontend
   git submodule add <backend-repo-url> conduit-backend
   ```

3. Add the required configuration files:

   - `.env` for environment variables.
   - `.gitignore` to exclude unnecessary files.
   - `.dockerignore` to ignore unneeded files during image builds.

4. Create the Dockerfiles:

   - **Frontend Dockerfile:** Builds the Angular application in one stage and serves it using Nginx.
   - **Backend Dockerfile:** Sets up a Python environment, installs dependencies, and runs the Django development server.

5. Define the `docker-compose.yaml`:

   - Configures two services (`conduit-frontend` and `conduit-backend`).
   - Exposes ports and maps them to the host.
   - Uses volumes for persistent data.

6. Make necessary changes to the backend settings (e.g., add allowed hosts).

7. Build and start the application:
   ```bash
   docker-compose up --build
   ```

## Troubleshooting

Common commands for diagnosing issues:

- View logs:
  ```bash
  docker-compose logs
  ```
- Rebuild containers:
  ```bash
  docker-compose up --build
  ```
- Remove stopped containers and volumes:
  ```bash
  docker-compose down -v

  ```
