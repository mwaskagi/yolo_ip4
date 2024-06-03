# lite image
FROM node:16-alpine  

LABEL maintainer="James Mwangi <gituiku.mwangi@gmail.com>"

# set working directory
WORKDIR /app

#ENV PATH /app/node_modules/.bin:$PATH

# install app dependencies
COPY package*.json ./


RUN npm install

# add app
COPY . .

#expose port
EXPOSE 5000

# start app
CMD ["npm", "start"]