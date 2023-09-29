pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker')
        IMAGE_NAME = "kvrae/alpine:2.0.0"
        DOCKERFILE_PATH = "Dockerfile"
    }
    stages {
        stage('Build and Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker') {
                        def customImage = docker.build("${env.IMAGE_NAME}", "--file=${env.DOCKERFILE_PATH} .")
                        customImage.push()
                    }
                }
            }
        }
    }
}
