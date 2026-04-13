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
}
}
