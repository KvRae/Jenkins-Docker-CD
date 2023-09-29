pipeline {
    environment {
        registry = "kvrae/dockerPipe"
        registryCredential = ''
        dockerImage = ''
    }
    agent any
    stages {
        stage('Cloning git Repo') {
            steps {
                git 'https://github.com/KvRae/Jenkins-Docker-CD.git'
            }
        }
        stage('Builing our image') {
            steps {
                script {
                    dockerImage = docker.build registry + "$BUILD_NUMBER"
                }
            }
        }
        stage('Cleaning up') {
            steps {
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        }
    }
}
