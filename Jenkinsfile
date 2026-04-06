pipeline {
    agent any

    environment {
        IMAGE_NAME = "rachita06/devops-proj"
        IMAGE_TAG = "v1"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Check Files') {
            steps {
                sh '''
                ls -ltr
                docker --version
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                dir('blog') {
                    sh '''
                    docker build -t $IMAGE_NAME:$IMAGE_TAG .
                    '''
                }
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-06',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    '''
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh '''
                docker push $IMAGE_NAME:$IMAGE_TAG
                '''
            }
        }

        stage('Logout Docker') {
            steps {
                sh 'docker logout'
            }
        }
    }
}
