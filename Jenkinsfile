pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "api-image"
        CONTAINER_NAME = "api-cntr"
        PORT = "3000"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo "Checked out code from repository"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                   // Build the Docker image
                    sh "docker build -t ${DOCKER_IMAGE} ."
                }
            }
        }

        stage('Stop Old Container') {
            steps {
                script {
                    // Stop and remove old container if it exists
                    sh """
                        docker stop ${CONTAINER_NAME} || true
                        docker rm ${CONTAINER_NAME} || true
                    """
                }
            }
        }
        
        stage('Deploy') {
            steps {
                 // Run the new container

                    sh """
                        docker run -d \
                        --name ${CONTAINER_NAME} \
                        -p ${PORT}:${PORT} \
                        --env-file /home/docker/api/.env \
                        ${DOCKER_IMAGE}:latest
                    """
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
            echo "Application deployed and running on port ${PORT}"
        }
        failure {
             echo 'Deployment failed!'
        }
         always {
            echo 'Cleaning up workspace...'
            cleanWs()
        }
    }
}