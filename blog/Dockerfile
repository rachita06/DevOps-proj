FROM jenkins/jenkins:lts

USER root

# Install docker client only (no daemon needed)
RUN apt-get update && \
    apt-get install -y docker.io && \
    apt-get clean

USER jenkins
