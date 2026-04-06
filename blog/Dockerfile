FROM ubuntu:22.04

# Install Java, Docker, Git, Curl
RUN apt-get update && \
    apt-get install -y openjdk-11-jdk docker.io git curl && \
    apt-get clean

# Download latest Jenkins LTS war
RUN curl -fsSL https://get.jenkins.io/war-stable/latest/jenkins.war -o /usr/share/jenkins.war

WORKDIR /app

# Run Jenkins
CMD ["java", "-jar", "/usr/share/jenkins.war"]
