# Has a small image
FROM node:16-alpine

# Label
LABEL maintainer="James Mwangi <gituiku.mwangi@gmail.com>"

# set working directory
WORKDIR /app

# i#Copy package.json file in the node folder inside container
COPY package*.json ./

# Install the dependencies in the container
RUN npm install

# Copy cdde to the container
COPY . .

#EXPOSE service over port 3000
EXPOSE 3000

# start app
CMD ["npm", "start"]