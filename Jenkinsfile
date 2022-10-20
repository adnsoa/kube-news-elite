pipeline {
    agent any

    stages {
        stage ("Build Docker Image") {
            steps {
                script {
                    dockerapp = docker.Build("adnsoa/kube-news-elite:${env.BUILD_ID}", '-f ./scr/Dockerfile ./scr' )
                }
            }
        }
    }
}