pipeline {
    agent any

    stages {

        stage('Clean Workspace') {
            steps {
                deleteDir()
            }
        }

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

    }
  }
