
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
            sh '''
           cd blog && docker build --no-cache -t blogimg01:v1 .
           docker image tag blogimg01:v1 rachita06/blogimg01:v1
           
          echo $DOCKER_PASS |  docker login -u $DOCKER_USER --password-stdin
           docker push rachita06/blogimg01:v1
           docker logout
            '''
		}

}
 		}
stage('Copy deploy.yaml to Kubernetes Server') {
steps {
sh 'scp deploy.yaml raj242adk@10.128.0.14:/home/raj242adk/'
}
}

}
}

