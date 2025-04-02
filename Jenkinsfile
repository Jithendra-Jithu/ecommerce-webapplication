pipeline {
    agent any
    
    environment {
        
        
        REGISTRY = 'jthu145/my-ecommerce:latest'
    }
    
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Jithendra-Jithu/ecommerce-webapplication.git'            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'cd backend && docker build -t ${REGISTRY} .'
                }
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'fb16b1ba-d2e9-41bb-8654-d00d3b5b61e6', url: '']) {
                   
                    sh 'docker push ${REGISTRY}'
                }
            }
        }
        
        stage('Deploy to Local Docker') {
            steps {
                script {
                    sh '''
                    docker stop ecommerce || true
                    docker rm ecommerce || true
                    docker run -d -p 5000:5000 --name ecommerce ${REGISTRY}
                    '''
                }
            }
        }
    }
    
    post {
        success {
            echo "✅ Deployment Successful!"
        }
        failure {
            echo "❌ Deployment Failed!"
        }
    }
}
