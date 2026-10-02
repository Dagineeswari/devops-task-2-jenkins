pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Pulling latest code from repository...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t my-app:latest .'
            }
        }

        stage('Test') {
            steps {
                echo 'Running basic tests...'
                sh 'docker run --rm my-app:latest nginx -t'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh 'docker stop my-app-container || true'
                sh 'docker rm my-app-container || true'
                sh 'docker run -d --name my-app-container -p 8080:80 my-app:latest'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check build logs.'
        }
    }
}
