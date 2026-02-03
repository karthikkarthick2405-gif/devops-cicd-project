pipeline {
    agent any

    environment {
        EC2_USER = "ubuntu"
        EC2_HOST = "51.21.181.68"
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
                ssh -o StrictHostKeyChecking=no ${EC2_USER}@${EC2_HOST} '
                    docker rm -f ${APP_NAME} || true
                    docker run -d -p ${APP_PORT}:5000 --name ${APP_NAME} ${APP_NAME}:latest
                '
                """
            }
        }
    }
}
