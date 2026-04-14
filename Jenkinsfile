pipeline {
    agent any

    environment {
        IMAGE_NAME = "cicd-staging-demo"
        CONTAINER_NAME = "staging-container"
    }

    stages {

        stage('Build Image') {
            steps {
                bat "docker build -t %IMAGE_NAME% ."
            }
        }

        stage('Stop Old Container') {
            steps {
                bat "docker stop %CONTAINER_NAME% || exit 0"
                bat "docker rm %CONTAINER_NAME% || exit 0"
            }
        }

        stage('Deploy') {
            steps {
                bat "docker run -d -p 5000:5000 --name %CONTAINER_NAME% %IMAGE_NAME%"
            }
        }

        stage('Test') {
            steps {
                bat "curl http://localhost:5000"
            }
        }
    }
}
