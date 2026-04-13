pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "rachita06/DevOps-proj"
        DOCKER_TAG = "latest"
    }

    options {
        skipDefaultCheckout(true)
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/rachita06/DevOps-proj.git',
                    credentialsId: 'git-06'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh """
                docker build -t blogimg01:lts .
                """
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-06',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh """
                    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    """
                }
            }
        }

        stage('Push Image') {
            steps {
                sh """
                docker push blogimg01:lts
                """
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh """
                kubectl apply -f deploy.yaml
                kubectl apply -f service.yaml
                """
            }
        }
    }

    post {
        success {
            echo " Deployment Successful!"
        }
        failure {
            echo " Pipeline Failed!"
        }
    }
}
