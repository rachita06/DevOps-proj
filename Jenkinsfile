pipeline {
    agent any

    stages {

    stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/rachita06/DevOps-proj.git',
                    credentialsId: 'git-06'
            }
        }

        stage('Check Files') {
            steps {
                sh 'ls -ltr'
                sh 'sudo docker ps'
            }
        }

        stage('Build & Push Docker Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-06',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                    cd blog && sudo  docker build -t DevOps-proj .
                   sudo docker tag DevOps-proj rachita06/DevOps-proj:v1

                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                   sudo docker push rachita06/DevOps-proj:v1
                   sudo docker logout
                    '''
                }
            }
        }
    }
