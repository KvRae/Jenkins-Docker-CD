pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('Docker')
        IMAGE_NAME = "kvrae/alpine_pip:1.0.0"
        GITHUB_REPO_URL = "https://github.com/KvRae/Jenkins-Docker-CD.git"
    }
    }
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: env.GITHUB_REPO_URL]]])
            }
        }
        stage('Build and Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials-id') {
                        def customImage = docker.build("${env.IMAGE_NAME}", "--file=Dockerfile .")
                        customImage.push()
                    }
                }
            }
        }
    }
}
