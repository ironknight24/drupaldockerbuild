pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = "drupal-site"
        DOCKER_IMAGE_TAG = "${env.BUILD_NUMBER}"
        // Replace with your Docker Hub username or private registry URL
        DOCKER_REGISTRY = "your-docker-registry"
    }

    stages {
        stage('Checkout') {
            steps {
                // Use a script block for more complex operations like shallow clone
                script {
                    // Add the shallow clone extension to the SCM object
                    scm.extensions << [$class: 'CloneOption', shallow: true]
                    // Checkout the modified SCM
                    checkout scm
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                withEnv(['PATH+PATH=/usr/local/bin']) {
                    script {
                        echo "Building Docker image: ${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}"
                        sh 'echo "Current user: $(whoami)"'
                        sh 'echo "PATH: $PATH"'
                        docker.build("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}")
                    }
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Make sure you have configured Docker credentials in Jenkins
                    // In a real-world scenario, you would use withCredentials to handle secrets
                    echo "Pushing Docker image to ${DOCKER_REGISTRY}"
                    // docker.withRegistry("https://" + DOCKER_REGISTRY, "docker-hub-credentials-id") {
                    //    docker.image("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}").push()
                    // }
                    echo "(Skipping push for this example)"
                }
            }
        }

        stage('Cleanup') {
            steps {
                // Clean up the workspace after the build
                cleanWs()
            }
        }
    }

    post {
        success {
            echo "Pipeline succeeded!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}
