pipeline{
    agent any

    stages {
        stage('Checkout') {
            steps {
              git branch: 'main', url: 'https://github.com/olaruionut01/devops-demo.git'
            }
        }
        stage('Install Dependencies'){
            steps{
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run tests'){
            agent {
                docker {
                    image 'python:3.11-slim'
                }
            }
            steps{
                sh '''
                pip install -r requirements.txt
                python -m pytest
                '''
            }
        }

        stage('Build image') {
            steps{
                script{
                    IMAGE_NAME = "olaruionut01/devops-demo:${BUILD_NUMBER}"
                }
                sh "docker build -t ${IMAGE_NAME} ."
                sh "docker tag ${IMAGE_NAME} olaruionut01/devops-demo:latest"
            }
        }
        stage('Push image'){
            steps{
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    docker push olaruionut01/devops-demo:${BUILD_NUMBER}
                    docker push olaruionut01/devops-demo:latest
                    '''
                }
            }
        }
        stage('Run container'){
            steps{
                sh '''
                docker stop devops-container || true
                docker rm devops-container || true
                docker run -d -p 5000:5000 --name devops-container devops-demo
                '''
            }
        }

    }

}