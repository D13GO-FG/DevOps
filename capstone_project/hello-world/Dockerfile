FROM ubuntu

# Run dependencies to nodejs app and shh configuration
RUN apt-get update  -y \
    && apt-get upgrade -y \ 
    && apt-get install -y \
    ssh \
    sudo \
    software-properties-common \
    nodejs \
    npm

# Set /app as the default work directory
WORKDIR /app

# Install app dependencies
COPY package*.json ./

# Install npm dependencies
RUN npm install

# Copy all the project files to the working directory
COPY . .

# Run commands to create user with all persimmions 
RUN useradd -rm -d /home/webapp -s /bin/bash -g root -G sudo -u 1001 webapp
RUN echo webapp:12345 | chpasswd
RUN echo "webapp ALL=(ALL:ALL) NOPASSWD: ALL" |  EDITOR="tee -a"  visudo
RUN mkdir -p /home/webapp/.ssh

# run your app and start ssh
CMD service ssh start && npm start
