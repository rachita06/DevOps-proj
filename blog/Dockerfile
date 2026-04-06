# Use official Jenkins LTS image as base
FROM jenkins/jenkins:lts

# Switch to root to install packages
USER root

# Install Docker client and Git
RUN apt-get update && \
    apt-get install -y docker.io git curl && \
    apt-get clean

# Switch back to jenkins user
USER jenkins

# Set working directory
WORKDIR /var/jenkins_home
