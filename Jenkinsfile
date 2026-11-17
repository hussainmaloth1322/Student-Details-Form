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
                bat 'docker build -t student-form .'
            }
        }

        stage('Run Docker Container') {
            steps {
                // Remove an older container if it exists. The run command below
                // will still fail visibly if Docker itself is unavailable.
                bat 'docker rm -f student-form-container 2>NUL || exit /b 0'
                // Host port 8081 avoids the usual Jenkins UI port 8080.
                bat 'docker run -d -p 8081:80 --name student-form-container student-form'
            }
        }
    }

    post {
        success {
            echo 'Student form container started. Open http://localhost:8081'
        }
    }
}
