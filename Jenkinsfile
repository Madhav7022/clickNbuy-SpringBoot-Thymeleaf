pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Madhav7022/clickNbuy-SpringBoot-Thymeleaf.git',
                    credentialsId: 'github-token'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t clicknbuy-app .'
            }
        }

        stage('Run Docker Container') {
            steps {
        // Stop old container if running
                sh 'docker rm -f clicknbuy-app || true'
        // Free port 8080 if any process is using it
                sh 'sudo fuser -k 8080/tcp || true'
        // Start new container
                sh 'docker run -d --name clicknbuy-app -p 9090:8080 clicknbuy-app'
            }
        }

    }
}
