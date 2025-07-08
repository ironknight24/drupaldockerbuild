pipeline {
    agent any

    options {
        // Skip the default checkout so we can perform a manual, shallow one.
        skipDefaultCheckout true
    }

    environment {
        DOCKER_IMAGE_NAME = "drupal-site"
        DOCKER_IMAGE_TAG = "${env.BUILD_NUMBER}"
        // Replace with your Docker Hub username or private registry URL
        DOCKER_REGISTRY = "your-docker-registry"
    }

    stages {
        stage('Checkout') {
            steps {
                // Manually perform a shallow checkout.
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    extensions: [[$class: 'CloneOption', shallow: true]],
                    userRemoteConfigs: [[url: 'https://github.com/ironknight24/drupaldockerbuild.git']]
                ])
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
