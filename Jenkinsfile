pipeline {
    agent any

    environment {
        IMAGE_NAME = 'my-app'
        IMAGE_TAG  = "${env.BUILD_NUMBER}"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/vedant1844/docker_jenkins_demo.git'
                // For a private repo, add: credentialsId: 'github-credentials'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:${IMAGE_TAG} -t ${IMAGE_NAME}:latest .'
            }
        }

        stage('Verify Image') {
            steps {
                sh 'docker images ${IMAGE_NAME}'
            }
        }

        stage('Build Message') {
            steps {
                echo "Build #${env.BUILD_NUMBER} completed. Image ${IMAGE_NAME}:${IMAGE_TAG} created."
            }
        }
    }

    post {
        failure {
            echo 'Build failed. Check the console output for details.'
        }
    }
}
