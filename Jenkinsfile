
pipeline {
    agent any

    stages {

        stage('Git Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/hussainmaloth1322/Student-Details-Form.git'
            }
        }

        stage('Check Docker') {
            steps {
                bat 'docker --version'
                bat 'docker info'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t student-details-app .'
            }
        }

        stage('Remove Old Container') {
            steps {
                bat 'docker rm -f student-details || exit /b 0'
            }
        }

        stage('Run Docker Container') {
            steps {
                bat 'docker run -d --name student-details -p 8081:80 student-details-app'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat 'docker ps'
            }
        }
    }

    post {
        success {
            echo 'Student Details Form deployed successfully!'
            echo 'Application URL: http://localhost:8081'
        }

        failure {
            echo 'Build or deployment failed. Check Jenkins Console Output.'
        }
    }
}
