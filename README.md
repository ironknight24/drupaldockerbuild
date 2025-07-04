# Drupal Docker Environment

This project uses Docker to create a consistent development environment for the Drupal application.

## Prerequisites

*   Docker
*   Docker Compose

## Getting Started

1.  **Build the Docker images:**

    ```bash
    docker-compose build
    ```

    This command builds the Docker image for the Drupal application as defined in the `Dockerfile`.

2.  **Start the services:**

    ```bash
    docker-compose up -d
    ```

    This command starts the Drupal application and the MySQL database in detached mode.

3.  **Access the site:**

    Once the containers are running, you can access your Drupal site at [http://localhost:8080](http://localhost:8080).

## Stopping the Environment

To stop the running services, use the following command:

```bash
docker-compose down
```

This will stop and remove the containers.
