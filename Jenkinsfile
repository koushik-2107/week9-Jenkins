
pipeline {
    agent any

    tools {
        maven 'MAVEN-HOME'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Test') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar',
                                 fingerprint: true
            }
        }
    }

    post {
        success {
            emailext(
                to: 'gummadavellikoushik2107@gmail.com',
                subject: "SUCCESS: ${JOB_NAME} #${BUILD_NUMBER}",
                body: """Build successful.

Job: ${JOB_NAME}
Build: ${BUILD_NUMBER}
Status: SUCCESS
URL: ${BUILD_URL}"""
            )
        }

        failure {
            emailext(
                to: 'gummadavellikoushik2107@gmail.com',
                subject: "FAILED: ${JOB_NAME} #${BUILD_NUMBER}",
                body: """Build failed.

Job: ${JOB_NAME}
Build: ${BUILD_NUMBER}
Status: FAILURE
URL: ${BUILD_URL}

Check the Jenkins Console Output."""
            )
        }
    }
}
