pipeline {
    agent {
        docker {
            image 'python:3.12'
        }
    }
    environment {
        DOCKER_IMAGE = "fastapi-app"
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/username/fastapi-jenkins-demo.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }
        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 8000:8000 $DOCKER_IMAGE'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'pip install pytest'
                sh 'pytest tests/'
            }
        }
        stage('Clean Up') {
            steps {
                sh 'docker stop $(docker ps -q --filter ancestor=$DOCKER_IMAGE)'
                sh 'docker rmi $DOCKER_IMAGE'
            }
        }
    }
}

