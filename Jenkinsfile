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
                sh 'docker rm -f clicknbuy-app || true'
                sh 'docker run -d --name clicknbuy-app -p 8080:8080 clicknbuy-app'
            }
        }
    }
}
