pipeline {
    agent any
     options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }

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
                sh 'docker ps'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-06',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Build Image') {
            steps {
                sh 'cd blog && docker build -t blogimg01 .'
            }
        }

        stage('Tag the image') {
            steps {
                sh 'docker image tag blogimg01 rachita06/blogimg01:v1'
            }
        }

        stage('Push the iamge to Docker Hub') {
            steps {
                sh 'docker push rachita06/blogimg01:v1'
                sh 'docker logout'
            }
        }

        stage('Copy deploy.yaml to Kubernetes Server') {
            steps {
                sshagent(['ssh-key-id']) {
                    sh '''
                    scp -o StrictHostKeyChecking=no *.yaml raj242adk@34.134.162.124:/home/raj242adk/
                    '''
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sshagent(['ssh-key-id']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no raj242adk@34.134.162.124 "
                    cd /home/raj242adk/
                    export KUBECONFIG=/home/raj242adk/admin.conf
                    kubectl apply -f deploy.yaml
                    kubectl apply -f service.yaml
                    "
                    '''
                }
            }
        }
    }
}
