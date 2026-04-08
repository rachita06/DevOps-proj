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
	      sh ' docker ps'
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
             sh 'cd blog &&  docker build -t blogimg01 .'
	     }
	     }
stage('Tag the image') {
steps {
sh 'docker tag blogimg01 rachita06/blogimg01:v1'
}
}
stage('Push the iamge to Docker Hub') {
steps {
// sh 'echo "$DOCKER_PASS" |  docker login -u "$DOCKER_USER" --password-stdin'
sh ' docker push rachita06/blogimg01:v1'
sh ' docker logout'
}
}


}
}
