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

        stage('Upload to Nexus') {
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: 'localhost:8081',
                    groupId: 'com.example',
                    version: '1.0-SNAPSHOT',
                    repository: 'maven-snapshots',
                    credentialsId: 'nexus-credentials',
                    artifacts: [
                        [artifactId: 'maven-jenkins-demo',
                         classifier: '',
                         file: 'target/maven-jenkins-demo-1.0-SNAPSHOT.jar',
                         type: 'jar']
                    ]
                )
            }
        }
    }

    post {
        success {
            echo 'Artifact uploaded to Nexus successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}