pipeline {
    agent any
     options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/susigugh/proj-feb.git',
                    credentialsId: 'git-01'
            }
        }
}
}
