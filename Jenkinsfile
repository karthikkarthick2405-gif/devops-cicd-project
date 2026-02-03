pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-cicd-app -f docker/Dockerfile .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker rm -f devops-cicd-app || true
                docker run -d -p 5000:5000 --name devops-cicd-app devops-cicd-app
                '''
            }
        }
    }
}
