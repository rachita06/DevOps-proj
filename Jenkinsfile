pipeline {
    agent any

    stages {

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-cred',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    '''
                }
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t blogimg01 .'
            }
        }

        stage('Tag Image') {
            steps {
                sh 'docker tag blogimg01 rachita06/blogimg01:v1'
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push rachita06/blogimg01:v1'
            }
        }
    }
}
