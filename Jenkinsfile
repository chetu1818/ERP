pipeline {
    agent any
    environment {
        DOCKER_CRED = credentials('docker-hub-credentials')
        backrepo = 'chetan1818/idurar-backend'
        frontend = 'chetan1818/idurar-frontend'
    }
    stages {
        stage('Checkout code') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker Images') {
            steps {
                bat 'docker build -t %backrepo%:%BUILD_NUMBER% ./backend'
                bat 'docker build -t %frontend%:%BUILD_NUMBER% ./frontend'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                bat 'echo %DOCKER_CRED_PSW%| docker login -u %DOCKER_CRED_USR% --password-stdin'
                bat 'docker push %backrepo%:%BUILD_NUMBER%'
                bat 'docker push %frontend%:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}