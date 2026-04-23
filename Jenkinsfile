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

        stage('Docker Build & Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-06',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                    cd blog
                    docker build -t rachita06/blogimg01:v1 .
                    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    docker push rachita06/blogimg01:v1
                    docker logout
                    '''
                }
            }
        }

        stage('Copy K8s Files') {
            steps {
                sh '''
                scp -o StrictHostKeyChecking=no deploy.yaml raj242adk@10.128.0.18:/home/raj242adk/
                scp -o StrictHostKeyChecking=no service.yaml raj242adk@10.128.0.18:/home/raj242adk/
                '''
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                ssh -o StrictHostKeyChecking=no raj242adk@10.128.0.18 "
                kubectl apply -f /home/raj242adk/deploy.yaml &&
                kubectl apply -f /home/raj242adk/service.yaml &&
                kubectl get pods &&
                kubectl get svc
                "
                '''
            }
        }
    }
}
