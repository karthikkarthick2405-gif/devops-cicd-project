pipeline {
    agent any

    environment {
        EC2_USER = "ubuntu"
        EC2_HOST = "16.171.206.83"
        APP_NAME = "devops-cicd-app"
        APP_PORT = "5000"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${APP_NAME}:latest -f docker/Dockerfile .'
            }
        }

        
        stage('Deploy to EC2') {
    steps {
        sh """
        ssh -o StrictHostKeyChecking=no ubuntu@51.21.181.68 '
            cd /home/ubuntu || exit 1
            rm -rf devops-cicd-project || true
            git clone https://github.com/karthikkarthick2405-gif/devops-cicd-project.git
            cd devops-cicd-project
            docker build -t devops-cicd-app:latest -f docker/Dockerfile .
            docker rm -f devops-cicd-app || true
            docker run -d -p 5000:5000 --name devops-cicd-app devops-cicd-app:latest
        '
        """
    }
}

    }
}
