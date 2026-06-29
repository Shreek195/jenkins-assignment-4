pipeline {
    agent any

    environment {
        // Replace with the exact ID of the credentials you created in Jenkins
        DOCKER_CRED = credentials('assignment4-jenkins') 
    }

    stages {
        stage('fetch-code') {
            steps {
                // Replace branch name (e.g., 'main') and your GitHub repository URL
                git branch: 'main', url: 'https://github.com/Shreek195/jenkins-assignment-4.git'
            }
        }

        stage('build-image') {
            steps {
                // Replace with your Docker Hub username and your desired image name
                sh "docker build -t shreek195/assignment-4:${BUILD_NUMBER} ."
            }
        }

        stage('push-image') {
            steps {
                // Replace with your Docker Hub username
                sh 'echo "$DOCKER_CRED_PSW" | docker login -u shreek195 --password-stdin'
                
                // Replace with your Docker Hub username and image name
                sh "docker push shreek195/assignment-4:${BUILD_NUMBER}"
            }
        }
        
        stage('update-minikube') {
            steps {
                // Replace deployment name, container name, Docker Hub username, and image name
                sh "kubectl set image deployment/assignment4-demo1 assignment-4=shreek195/assignment-4:${BUILD_NUMBER}"
            }
        }
    }
}