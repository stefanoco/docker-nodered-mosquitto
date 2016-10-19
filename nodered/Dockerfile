# As found here: https://gist.github.com/dceejay/9435867
#
# Dockerfile for Node-RED - pulls latest master code from git
# Use the node.js v0.10.36 engine
FROM node:0.12-slim
MAINTAINER ceejay

# add git
RUN apt-get update
RUN apt-get install -y git

# download latest stable node-red
RUN npm install -g node-red

# add some useful nodes
RUN npm install -g node-red/node-red-dashboard
RUN npm install -g node-red-node-random
RUN npm install -g node-red-contrib-graphs

# use external storage for the user directory
VOLUME /root/.node-red

# expose port
EXPOSE 1880

# Set the default command to execute
# when creating a new container
CMD /usr/local/bin/node-red -v
