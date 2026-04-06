FROM jenkins/jenkins:lts

USER root

# Install docker client
RUN apt-get update && \
    apt-get install -y docker.io git curl && \
    apt-get clean

USER jenkins
WORKDIR /var/jenkins_home
