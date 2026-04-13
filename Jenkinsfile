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
stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-06',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )])
		{
            sh 'echo $DOCKER_PASS |  docker login -u $DOCKER_USER --password-stdin'
        }
		}
		}
      
      stage('Build Image') {
      steps {
             sh 'cd blog &&  ls -ltr && sudo docker build -t blogimg01.'
	     }
         	     }
}
}
