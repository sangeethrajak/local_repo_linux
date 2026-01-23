pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t html-nginx-app:latest .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker stop nginx-html || true
                docker rm nginx-html || true
                docker run -d -p 8085:80 --name nginx-html html-nginx-app:latest
                '''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'index.html,Dockerfile,Jenkinsfile', fingerprint: true
        }
    }
}

