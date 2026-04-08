pipeline {
    agent any

    environment {
        // Optional: define global variables if needed
    }

    stages {

        stage('Checkout from GitHub') {
            steps {
                // Use credentials for GitHub if repo is private
                git branch: 'main', 
                    url: 'https://github.com/rachita06/DevOps-proj.git', 
                    credentialsId: 'git-06'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-06',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    '''
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t blogimg01 .'
            }
        }

        stage('Tag Docker Image') {
            steps {
                sh 'docker tag blogimg01 rachita06/blogimg01:v1'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push rachita06/blogimg01:v1'
            }
        }
    }

    post {
        failure {
            echo "Pipeline failed. Check logs for errors."
        }
        success {
            echo "Pipeline completed successfully!"
        }
    }
}
