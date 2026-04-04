pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git(
                    branch: 'master',
                    url: 'https://github.com/rachita06/DevOps-proj.git',
                    credentialsId: 'git-06'
                )
            }
        }

        stage('Check Files') {
            steps {
                sh 'ls -ltr'
                sh 'docker ps'
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
                        cd blog
                        docker build -t DevOps-proj .
                        docker tag DevOps-proj rachita06/DevOps-proj:v1

                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push rachita06/DevOps-proj:v1
                        docker logout
                    '''
                }
            }
        }
    }
}
