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
	      sh 'sudo docker ps'
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
            sh 'echo $DOCKER_PASS | sudo docker login -u $DOCKER_USER --password-stdin'
        }
		}
		}
      
      stage('Build Image') {
      steps {
             sh 'cd blog && sudo docker build -t blogimg01 .'
	     }
	     }
stage('Tag the image') {
steps {
sh 'sudo docker image tag blogimg01 rachita06/blogimg01:v1'
}
}
stage('Push the iamge to Docker Hub') {
steps {
// sh 'echo "$DOCKER_PASS" | sudo docker login -u "$DOCKER_USER" --password-stdin'
sh 'sudo docker push rachita06/blogimg01:v1'
sh 'sudo docker logout'
}
}

stage('Copy deploy.yaml to Kubernetes Server') {
steps {
sh 'chmod 600 id_rsa'
sh 'scp -o StrictHostKeyChecking=no -i id_rsa *.yaml raj242adk@10.128.0.18:/home/raj242adk/'
}
}


stage('Deploy the deployment in Kubernetes Server') {
steps {
sh 'chmod 600 id_rsa'
sh 'ssh -o StrictHostKeyChecking=no -i id_rsa raj242adk@10.128.0.18 "cd /home/raj242adk/ && export KUBECONFIG=/home/raj242adk/admin.conf && kubectl create -f deploy.yaml"'
}
}

stage('Create the service in Kubernetes Server') {
steps {
sh 'chmod 600 id_rsa'
sh 'ssh -o StrictHostKeyChecking=no -i raj242adk@10.128.0.18 "cd /home/raj242adk/ && export KUBECONFIG=/home/raj242adk/admin.conf && kubectl create -f service.yaml"'
}
}


}
}
