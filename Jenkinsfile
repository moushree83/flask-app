pipeline {
    agent any

    stages {
        stage('Pull from GitHub') {
            steps {
                git 'https://github.com/moushree83/flask-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-cicd .'
            }
        }

        stage('Stop & Remove Old Container') {
            steps {
                sh '''
                docker stop flask-cicd-container || true
                docker rm flask-cicd-container || true
                '''
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d -p 5001:5000 --name flask-cicd-container flask-cicd'
            }
        }
    }
}
