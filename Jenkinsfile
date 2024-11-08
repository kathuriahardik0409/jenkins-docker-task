pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = 'kathuriahardik'
        IMAGE_NAME = 'kathuriahardik/docker-jenkins-task'
        GIT_REPO_URL = 'https://github.com/kathuriahardik0409/jenkins-docker-task.git'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: "${GIT_REPO_URL}", branch: 'master'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image with a unique tag
                    docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_HUB_CREDENTIALS) {
                        // Push the latest tag to Docker Hub
                        docker.image("${IMAGE_NAME}:latest").push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
