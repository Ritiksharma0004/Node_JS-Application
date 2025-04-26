pipeline {
    agent any

    environment {
        IMAGE_NAME = 'mohitsingh0001/node-docker-app'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/mohitsingh0008/Node_JS-Application'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    script {
                        docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
                            docker.image("${IMAGE_NAME}").push('latest')
                        }
                    }
                }
            }
        }
    }
}
