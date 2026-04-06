pipeline {
    agent any

    environment {
        // Change 'yourusername' to your actual Docker Hub ID
        DOCKER_USER = 'srsuhtir'
        IMAGE_NAME = 'myapp'
        IMAGE_TAG = 'v1'
    }

    stages {
        stage('Checkout Code') {
            steps {
                // This pulls your code from GitHub
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    bat "docker build -t ${DOCKER_USER}/${IMAGE_NAME}:${IMAGE_TAG} ."
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                // 'dockerhub-creds' must match the ID you create in Jenkins Step 7
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', 
                                 passwordVariable: 'DOCKER_PASS', 
                                 usernameVariable: 'DOCKER_USER_VAR')]) {
                    bat "echo ${DOCKER_PASS} | docker login -u ${DOCKER_USER_VAR} --password-stdin"
                    bat "docker push ${DOCKER_USER}/${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }
    }
}
