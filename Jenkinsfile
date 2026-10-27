pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t jenkins-demo-app:%BUILD_NUMBER% -t jenkins-demo-app:latest .'
            }
        }

        stage('Deploy Container') {
            steps {
                bat 'docker rm -f jenkins-demo-app 2>nul || exit /b 0'
                bat 'docker run -d --name jenkins-demo-app -p 9090:80 jenkins-demo-app:latest'
            }
        }
    }

    post {
        success {
            echo 'Docker image built and deployed on http://localhost:9090'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}