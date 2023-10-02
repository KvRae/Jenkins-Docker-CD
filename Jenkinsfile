pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("kvrae/alpine_jenkins:${env.BUILD_NUMBER}")
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'Docker') {
                        docker.image("kvrae/alpine_jenkins:${env.BUILD_NUMBER}").push()
                    }
                }
            }
        }
    }
}
