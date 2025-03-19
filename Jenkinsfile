
pipeline {
    agent any

    environment {
        IMAGE_NAME = "hariharan3104/my-app"
        REGISTRY = "docker.io"
        APP_DIR = "/home/hari/Downloads"
        DOCKER_USER = "hariharan3104"          // Replace with your Docker Hub username
        DOCKER_PASS = "H@ri_2004"          // Replace with your Docker Hub password
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/Hariharan-3104/Jenkins', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t $IMAGE_NAME:latest ."
                }
            }
        }

        stage('Login to Docker Registry') {
            steps {
                script {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Push Image to Docker Registry') {
            steps {
                script {
                    sh "docker push $IMAGE_NAME:latest"
                }
            }
        }

        stage('Deploy using Docker Compose') {
            steps {
                script {
                    sh "docker-compose up -d"
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed! Check the logs for errors.'
        }
    }
}
