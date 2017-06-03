FROM jenkins:latest

USER root

RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - && \
apt-get update -y && \
apt-get install apt-utils -y && \
apt-get install nodejs -y

