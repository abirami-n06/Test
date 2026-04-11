pipeline {
    agent any
    environment {
        ECR_REPO = '906286017958.dkr.ecr.ap-south-1.amazonaws.com/my-website'
        REGION = 'ap-south-1'
    }
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
        stage('Push to ECR') {
            steps {
                sh 'aws ecr get-login-password --region ${REGION} | docker login --username AWS --password-stdin ${ECR_REPO}'
                sh 'docker tag my-website:latest ${ECR_REPO}:latest'
                sh 'docker push ${ECR_REPO}:latest'
            }
        }
        stage('Run Container') {
            steps {
                sh 'docker stop my-website || true'
                sh 'docker rm my-website || true'
                sh 'docker run -d --name my-website --restart always -p 80:80 ${ECR_REPO}:latest'
            }
        }
    }
}
