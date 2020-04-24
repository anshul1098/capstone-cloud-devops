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
                    steps {
                        sh 'sudo docker login --username anshul1098 --password-stdin < ~/my_password.txt'
                        sh 'sudo docker build -t anshul1098/blueimage -f blue-green/blue/Dockerfile blue-green/blue'
                        sh 'sudo docker build -t anshul1098/greenimage -f blue-green/green/Dockerfile blue-green/green'
                        sh 'sudo docker push anshul1098/blueimage'
                        sh 'sudo docker push anshul1098/greenimage'
                        sh 'sudo docker rmi -f anshul1098/greenimage'
                        sh 'sudo docker rmi -f anshul1098/blueimage'
                    }
                }
    }
}
