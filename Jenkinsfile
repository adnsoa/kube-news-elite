pipeline {
    agent any

    stages {

        stage ('Build Docker Image') {
            steps {
                script {
                    dockerapp = docker.build("adnsoa/kube-news-elite:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
                }
            }
        }

        stage ('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com','dockerhub') {
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }                    
                }
            }
        }


        stage ('Deploy Kubernetes') {
            steps {
                withkubeConfig ([credentialsId: 'kubeconfig']) {
                    sh 'kubeclt apply -f ./k8s/deployment.yaml'
                }                
            }
        }
    }

}