pipeline {
    agent any

    tools {
        maven 'Maven-3.9.16'
    }

    stages {
        stage('Notify Start') {
            steps {
                slackSend(
                    channel: '#jenkins-notifications',
                    tokenCredentialId: 'slack-token',
                    botUser: true,
                    color: '#439FE0',
                    message: "STARTED: Job '${env.JOB_NAME}' build #${env.BUILD_NUMBER} (${env.BUILD_URL})"
                )
            }
        }

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
    }

    post {
        success {
            slackSend(
                channel: '#jenkins-notifications',
                tokenCredentialId: 'slack-token',
                botUser: true,
                color: 'good',
                message: "SUCCESS: Job '${env.JOB_NAME}' build #${env.BUILD_NUMBER} (${env.BUILD_URL})"
            )
        }
        failure {
            slackSend(
                channel: '#jenkins-notifications',
                tokenCredentialId: 'slack-token',
                botUser: true,
                color: 'danger',
                message: "FAILED: Job '${env.JOB_NAME}' build #${env.BUILD_NUMBER} (${env.BUILD_URL})"
            )
        }
    }
}