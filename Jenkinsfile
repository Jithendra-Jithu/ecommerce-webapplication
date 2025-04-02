pipeline {
    agent any
       environment {
    DOCKER_CREDENTIALS = 'fb16b1ba-d2e9-41bb-8654-d00d3b5b61e6'
       }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Jithendra-Jithu/ecommerce-webapplication.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jithu145/ecommerce-backend:latest backend/'
            }
        }

       stage('Push to Docker Hub') {
    steps {
        script {
            withCredentials([usernamePassword(credentialsId: DOCKER_CREDENTIALS, passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                // Login securely using --password-stdin
                sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'

                    sh 'docker push jithu145/ecommerce-backend:latest'
                }
            }
        }
       }

        stage('Deploy') {
            steps {
                sh 'docker run -d -p 5000:5000 jithu154/ecommerce-backend:latest'
            }
        }
    }
}


