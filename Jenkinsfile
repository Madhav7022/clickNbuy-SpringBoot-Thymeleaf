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
                // Remove old app container if exists
                sh 'docker rm -f clicknbuy-app || true'
                
                // Run App container with DB connection details
                // We use the Host IP (172.31.1.146) to connect to the mysql-db container we just started
                sh '''
                    docker run -d --name clicknbuy-app -p 8081:8080 \
                    -e SPRING_DATASOURCE_URL=jdbc:mysql://172.31.1.146:3306/clicknbuy \
                    -e SPRING_DATASOURCE_USERNAME=root \
                    -e SPRING_DATASOURCE_PASSWORD=root \
                    -e SPRING_JPA_HIBERNATE_DDL_AUTO=update \
                    clicknbuy-app
                '''
            }
        }

    }
}
