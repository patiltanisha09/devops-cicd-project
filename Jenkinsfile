pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                echo 'Cloning source code from GitHub'
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t devops-app .'
            }
        }

        stage('Run Docker Container') {
            steps {
                bat 'docker rm -f devops-container >nul 2>&1 || exit /b 0'
                bat 'docker run -d --name devops-container -p 8081:80 devops-app'
            }
        }

        stage('Verify Application') {
            steps {
                bat 'docker ps'
                bat 'curl --fail http://localhost:8081/'
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }

        failure {
            echo 'CI/CD Pipeline failed!'
        }
    }
}
              
