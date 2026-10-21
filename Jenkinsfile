
pipeline {
    agent any

    tools {
        jdk 'JDK21'
        maven 'MAVEN3'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo 'Source code checked out successfully'
            }
        }

        stage('Compile') {
            steps {
                bat 'mvn -B compile'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn -B test'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn -B package'
            }
        }
    }

    post {
        always {
            junit testResults: 'target/surefire-reports/*.xml',
                  allowEmptyResults: true
            archiveArtifacts artifacts: 'target/*.jar',
                             allowEmptyArchive: true
        }

        success {
            echo 'SUCCESS: Build, tests and packaging completed!'
        }

        failure {
            echo 'FAILURE: Check the Console Output.'
        }
    }
}
