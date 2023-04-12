FROM node:16-alpine as builder

# Set /app as the default work directory
WORKDIR /app

# Install app dependencies
COPY package*.json ./

# Install npm dependencies
RUN npm install

# Copy all the project files to the working directory
COPY . .

RUN npm run build

# Expose the port of your application to bind with the host port
EXPOSE 3000

# run your app
CMD [ "npm", "run", "start" ]
