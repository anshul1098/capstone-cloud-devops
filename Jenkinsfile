pipeline {
    agent any
    stages {
        stage('Lint HTML & Dockerfile'){
            steps {
                sh 'tidy -q -e blue-green/blue/*.html'
                sh 'tidy -q -e blue-green/green/*.html'
                sh 'hadolint blue-green/blue/Dockerfile'
                sh 'hadolint blue-green/green/Dockerfile'
            }
        }
        stage('Build and Publish Docker Image'){
            steps{        
                script{
                    docker.withRegistry('https://registry.hub.docker.com', 'docker') {
                    def blue = docker.build("anshul1098/blue-image","-f blue-green/blue/Dockerfile blue-green/blue")
                    def green = docker.build("anshul1098/green-image","-f blue-green/green/Dockerfile blue-green/green")
                    blue.push()
                    green.push()    
                    }
                }
            }
        }
        stage('Remove Unused docker image') {
            steps{
                sh 'sudo docker rmi -f anshul1098/greenimage'
                sh 'sudo docker rmi -f anshul1098/blueimage'
            }
        }
    }
}
