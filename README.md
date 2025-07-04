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

    Once the containers are running, the Nginx web server will be serving your Drupal site at [http://localhost:8082](http://localhost:8082).

## Stopping the Environment

To stop the running services, use the following command:

```bash
docker-compose down
```

This will stop and remove the containers.

## Jenkins Pipeline

This project includes a `Jenkinsfile` to automate the build process of the Docker image.

### How to Run the Jenkins Pipeline

1.  **Create a New Pipeline Job:**
    *   In your Jenkins dashboard, click on **New Item**.
    *   Enter a name for your pipeline (e.g., "drupal-docker-build").
    *   Select **Pipeline** and click **OK**.

2.  **Configure the Pipeline:**
    *   Scroll down to the **Pipeline** section.
    *   For **Definition**, select **Pipeline script from SCM**.
    *   For **SCM**, select **Git**.
    *   For **Repository URL**, enter the URL of your Git repository.
    *   For **Script Path**, make sure it's set to `Jenkinsfile` (which is the default).

3.  **Save and Run:**
    *   Click **Save**.
    *   Click on **Build Now** to run the pipeline.

### Important Notes:

*   **Docker Integration:** This `Jenkinsfile` assumes you have the **Docker Pipeline** plugin installed in Jenkins.
*   **Docker Credentials:** The "Push Docker Image" stage is commented out. To push to a Docker registry (like Docker Hub), you'll need to:
    1.  Store your Docker credentials in Jenkins (under **Manage Jenkins** > **Credentials**).
    2.  Uncomment the `docker.withRegistry` block in the `Jenkinsfile` and replace `"docker-hub-credentials-id"` with the ID of your credentials.
*   **`DOCKER_REGISTRY`:** Remember to replace `"your-docker-registry"` in the `Jenkinsfile` with your actual Docker Hub username or the URL of your private registry.

## Drush Commands

To run Drush commands within the Drupal container, use `docker-compose exec drupal vendor/bin/drush` followed by the desired Drush command.

*   **Clear Cache:**
    ```bash
    docker-compose exec drupal vendor/bin/drush cr
    ```

*   **Enable a Module:**
    ```bash
    docker-compose exec drupal vendor/bin/drush en <module_name> -y
    ```
    Replace `<module_name>` with the actual machine name of the module (e.g., `admin_toolbar`, `pathauto`).

*   **Uninstall a Module:**
    ```bash
    docker-compose exec drupal vendor/bin/drush pm:uninstall <module_name> -y
    ```
    Replace `<module_name>` with the actual machine name of the module.
