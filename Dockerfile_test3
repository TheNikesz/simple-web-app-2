# Specify a base image
FROM node:alpine

# Install ssh client and git
RUN apk add --no-cache openssh-client git

# Download public key for github.com
RUN mkdir -p -m 0600 ~/.ssh && ssh-keyscan github.com >> ~/.ssh/known_hosts

# Clone a private repository
RUN --mount=type=ssh git clone git@github.com:TheNikesz/simple-web-app.git simplewebapp

# Specify a working directory
WORKDIR /simplewebapp

# Install depenendencies
RUN npm install

# Default command
CMD ["npm", "start"]