# Start from a Node.js 10 image
FROM node:10

# Specify the directory(in container) inside which all commands will run
WORKDIR /usr/src/app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy all of the app files into the image
COPY . .

# The default command to run when starting the container
CMD [ "npm", "start" ]
