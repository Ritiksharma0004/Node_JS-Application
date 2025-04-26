pipeline {
    agent any

    environment {
        IMAGE_NAME = 'ritiksharma04/node-docker-app'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Ritiksharma0004/Node_JS-Application'
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
                    credentialsId: 'a2f1bccc-2e1a-4272-916c-956cd10d2788',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    script {
                        docker.withRegistry('https://index.docker.io/v1/', 'a2f1bccc-2e1a-4272-916c-956cd10d2788') {
                            docker.image("${IMAGE_NAME}").push('latest')
                        }
                    }
                }
            }
        }
    }
}
