FROM node:14

# seting the working dir
WORKDIR /usr/src/app

# copy all .json files to the working directory
COPY package*.json ./

# install depes
RUN npm install

# copy the application code
COPY . .

# expose the port 
EXPOSE 3000

# command to run the application
CMD ["node", "server.js"]
