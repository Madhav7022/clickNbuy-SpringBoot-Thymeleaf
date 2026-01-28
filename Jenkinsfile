pipeline {
    agent any

    tools {
        maven 'Maven_3.9'   // Configure Maven in Jenkins tools
        jdk 'Java_17'       // Configure Java in Jenkins tools
    }

    stages {
        stage('Checkout') {
            steps {
                // Pull code from GitHub
                git branch: 'main', url: 'https://github.com/Madhav7022/clickNbuy-SpringBoot-Thymeleaf.git'
            }
        }

        stage('Docker Build & Run') {
            steps {
                sh 'docker build -t clicknbuy-app .'
                sh 'docker run -d -p 8080:8080 clicknbuy-app'
            }
        }


        stage('Build') {
            steps {
                // Clean and build project
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                // Run unit tests
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                // Package into JAR
                sh 'mvn package'
            }
        }

        stage('Deploy') {
            steps {
                // Stop old app if running
                sh 'pkill -f clickNbuy-SpringBoot-Thymeleaf || true'
                // Start new app in background
                sh 'nohup java -jar target/clickNbuy-SpringBoot-Thymeleaf-0.0.1-SNAPSHOT.jar > app.log 2>&1 &'
            }
        }
    }
}
