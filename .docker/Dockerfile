FROM jenkins/jenkins:lts
USER root

RUN apt-get update

RUN curl -sL https://deb.nodesource.com/setup_12.x | bash
RUN apt install nodejs

RUN apt install python3-pip -y
RUN pip3 install awscli --upgrade

EXPOSE 8080
EXPOSE 50000

# RUN docker ps
# RUN node --version
# RUN npm --version
