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
                sh 'ls -ltr blog'
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
                    dir('blog') {   // make sure Dockerfile is in this folder
                        sh '''
                        docker build -t devops-proj .
                        docker tag devops-proj $DOCKER_USER/devops-proj:v1
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push $DOCKER_USER/devops-proj:v1
                        docker logout
                        '''
                    }
                }
            }
        }
    }
}
