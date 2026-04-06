pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/rachita06/DevOps-proj.git'
            }
        }

        stage('Check Files') {
            steps {
                sh 'ls -ltr'
                sh 'docker --version'
            }
        }

        stage('Build & Push Docker Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-06',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    dir('blog') {
                        sh '''
                        docker build -t rachita06/devops-proj:v1 .
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push rachita06/devops-proj:v1
                        docker logout
                        '''
                    }
                }
            }
        }

    }
}
