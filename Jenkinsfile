pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/karthikkarthick2405-gif/devops-cicd-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-cicd-app -f docker/Dockerfile .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                docker rm -f devops-flask || true
                docker run -d -p 5000:5000 --name devops-flask devops-cicd-app
                '''
            }
        }
    }
}
