pipeline{
    agent any

    stages {
        stage('Checkout') {
            steps {
              git branch: 'main', url: 'https://github.com/olaruionut01/devops-demo.git'
            }
        }

        stage('Build image') {
            steps{
                sh 'docker build -t devops-demo .'
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