pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/abirami-n06/Test.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-website:latest .'
            }
        }
        stage('Run Container') {
            steps {
                sh 'docker stop my-website || true'
                sh 'docker rm my-website || true'
                sh 'docker run -d --name my-website -p 80:80 my-website:latest'
            }
        }
    }
}
