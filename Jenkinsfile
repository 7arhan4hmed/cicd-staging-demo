pipeline {
    agent any

    environment {
        IMAGE_NAME = "cicd-staging-demo"
        CONTAINER_NAME = "staging-container"
    }

    stages {

        stage('Build Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Stop Old Container') {
            steps {
                sh "docker stop ${CONTAINER_NAME} || true"
                sh "docker rm ${CONTAINER_NAME} || true"
            }
        }

        stage('Deploy') {
            steps {
                sh """
                docker run -d -p 5000:5000 --name ${CONTAINER_NAME} ${IMAGE_NAME}:latest
                """
            }
        }

        stage('Test') {
            steps {
                sh "curl http://localhost:5000"
            }
        }
    }
}
