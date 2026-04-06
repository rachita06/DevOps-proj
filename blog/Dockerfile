FROM jenkins/jenkins:lts

USER root

# Install docker client (no daemon needed)
RUN apt-get update && \
    apt-get install -y docker.io git curl && \
    apt-get clean

USER jenkins
