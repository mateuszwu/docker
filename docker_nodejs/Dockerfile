FROM ubuntu:latest
ARG NODE_VERSION
RUN apt-get update && apt-get install -y wget build-essential
RUN wget http://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.xz
RUN tar -xJvf node-v$NODE_VERSION-linux-x64.tar.xz -C /usr/bin
RUN rm -f node-v$NODE_VERSION-linux-x64.tar.xz
ENV PATH "$PATH:/usr/bin/node-v$NODE_VERSION-linux-x64/bin/"
RUN npm install --global yarn
