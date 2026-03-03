pipeline {
    agent {
        docker {
            image 'python:3.11-slim'
        }
    }

    stages {
        stage('Check Python Version') {
            steps {
                sh 'python --version'
            }
        }
    }
}