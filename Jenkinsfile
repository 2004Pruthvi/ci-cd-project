pipeline {
    agent any

    stages {

        stage('Build Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ci-cd-app .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker stop ci-cd-container || true
                docker rm ci-cd-container || true
                docker run -d --name ci-cd-container -p 8081:8080 ci-cd-app
                '''
            }
        }

    }
}
