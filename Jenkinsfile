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
                // Remove existing container if it exists (ignore failure if it doesn't)
                sh 'docker rm -f clicknbuy-app || true'
                
                // Run new container mapping Host Port 8081 to Container Port 8080
                sh 'docker run -d --name clicknbuy-app -p 8081:8080 clicknbuy-app'
            }
        }

    }
}
