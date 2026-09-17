pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                echo 'Cloning source code from GitHub'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t devops-app .'
            }
        }

        stage('Run Docker Container') {
            steps {
                bat 'docker stop devops-container || exit 0'
                bat 'docker rm devops-container || exit 0'
                bat 'docker run -d --name devops-container -p 8081:80 devops-app'
            }
        }

        stage('Verify Application') {
            steps {
                bat 'docker ps'
                bat 'curl http://localhost:8081'
            }
        }
    }
}
