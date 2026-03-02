pipeline{
    agent any

    stages {
        stage('Checkout') {
            steps {
              git 'https://github.com/olaruionut01/devops-demo.git'
            }
        }

        stage('Build image') {
            steps{
                sh 'docker build -t devops-demo .'
            }
        }

        stage('Run containter'){
            steps{
                sh '''
                docker stop devops-containter || true
                docker rm devops-container || true
                docker run -d -p 5000:5000 --name devops-containter devops-demo
                '''
            }
        }

    }

}