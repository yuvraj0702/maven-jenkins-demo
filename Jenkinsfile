pipeline {
    agent any

    tools {
        maven 'Maven-3.9.16'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Snyk Security Scan') {
            steps {
                snykSecurity(
                    snykInstallation: 'snyk',
                    snykTokenId: 'snyk-token',
                    failOnIssues: false,
                    severity: 'high'
                )
            }
        }
    }

    post {
        success {
            echo 'Pipeline with Snyk scan completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}