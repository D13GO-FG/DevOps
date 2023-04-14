# DevOps Bootcamp Capstone Project

- [DevOps Bootcamp Capstone Project](#devops-bootcamp-capstone-project)
  - [Description](#description)
  - [Features and Requirements](#features-and-requirements)
  - [Guidelines](#guidelines)
  - [Resources](#resources)
  - [Pre-requisites](#pre-requisites)
  - [1. Setup your development environment](#1-setup-your-development-environment)
    - [Repository](#repository)
    - [Application](#application)
  - [2. Containerize the application](#2-containerize-the-application)
  - [3. Create a CI Pipeline](#3-create-a-ci-pipeline)
  - [4. Update "Hello World!" to "Hello DevOps!"](#4-update-hello-world-to-hello-devops)

## Description

In this project, you will be using some of the tools and technologies you have learned during the bootcamp.

## Features and Requirements

- Node Js application will be provided
- Containerization using docker
- CI pipeline using Github Actions (Including automated testing,build)
- Update the Node JS application content using Ansible

## Guidelines

- Instruction for the project will be available on Thursday, April 6th
- One week to deliver the project. Please deliver the project no later than Monday, April 17.
- Send the repo link or project to talent@itjuana.com
- After delivering the trainers will review the content, if you pass you’ll get a badge recognizing your knowledge as DevOps Engineer.
- You’ll know the results via email from the ITJ Talent Team.
- Any questions or comments, please post it in the [WhatsApp group](https://chat.whatsapp.com/KiirrKYAJ3SINrDn1pLZ7C)

## Resources

[Bootcamp Presentations](https://github.com/itjuana-bootcamp/DevOps/tree/main/Presentations)

## Pre-requisites

- [Docker](https://docs.docker.com/desktop/) installed
  - `docker --version` should show the docker version
- [Git](https://github.com/git-guides/install-git) installed
  - `git --version` should show the git version
- [Node JS](https://nodejs.org/en/download/package-manager/)
  - `npm version` should show the node version
- Have a [github account](https://github.com/join)
- Code editor of your preference - [VS Code](https://code.visualstudio.com/download) recommended

## 1. Setup your development environment

### Repository

- Go to the github repository https://github.com/itjuana-bootcamp/DevOps
- Fork the repository
  NOTE: From here on, whenever we say repository , that refers to your forked repository.
- Clone the repository : `git clone git@github.com:<githubaccount>/DevOps.git`

### Application

- Go to folder `hello-world`
- Run `npm install` .
- Run `npm test` . All tests need to pass.
- Run `npm start` to run the application.
- Check http://localhost:3000 is reachable and displaying "Hello World!"

---

## Done!!!!

---

## 2. Containerize the application

- Using docker, containerize the application.
- Build the container and run it to make the application available on http://localhost:3000

---

## Done!!!!

1.  Containerize using image from local project:

- First in hello world folder, in command line type:

```
docker build -t {name_image} .
```

- Then run run it in port 3000 using:

```
sudo docker run -it -p 3000:3000 -d {name_image}
```

2. Containerize using image from Ducker Hub:

- Current lastest version in my docker hub, type:

```
sudo docker run -it -p 3000:3000 -d ldiegoflores/devops_itj:0.1.0
```

3. Finally for both options open you favorite browser and go to the next url:

```
http://localhost:3000/
```

---

## 3. Create a CI Pipeline

- Create a CI pipeline which
  - will trigger on push and on pull request
  - Run the tests
  - Only if tests are success, build the container

---

## Done!!!!

- In the root of this project you'll find .github with [main.yml](/.github/workflows/main.yml) in workflows.
  - Trigger both push and pull request
  - Envirenment variables for docker username, password and repo name
  - Default work directory pointer to run all commands in right directory where is hello-world
  - Steps:
    - Run ubuntu latest
    - Install dependencies
    - Save version to create repository versibles in docker hub
    - Run test
    - If test pass
      - Login Docker Hub
      - Build Docker Image
      - Push to Docker Hub
- Finally you can get lastest image version in https://hub.docker.com/r/ldiegoflores/devops_itj/tags

---

## 4. Update "Hello World!" to "Hello DevOps!"

- Update the node js application to display "Hello DevOps!" instead of "Hello World!" using ansible.

---

## Done!!!!

- First I added folder ansible_base with the files [Dockerfile](/capstone_project/ansible_base/Dockerfile) and [startup.sh](/capstone_project/ansible_base/startup.sh)

- To achive this step is needed run Ansible in a container using [docker-compose.yml](/capstone_project/docker-compose.yml), typing:

```bash
cd capstone_project/
docker compose up
```

- Ones is runnig both the ansible_controller and hello_word containers, open your favorite browser and search:

```
http://localhost:3000/
```

- The Open a new terminal and get into the ansible_controller machine

```bash
docker exec -w /home/ansible_controller/ansible_files/ -ti ansible_controller bash
```

- Finally to change "Hello World!" to "Hello DevOps!" in App.js, you need to run the [playbook.yml](/capstone_project/ansible_files/playbook.yml) making use of [inventory.ini](/capstone_project/ansible_files/inventory.ini) using:

```bash
ansible-playbook -i inventory.ini playbook.yml
```

---

## Tips

To stop all running Docker containers, you can use either of these commands:

```
docker stop $(docker container ls -q)
```

To delete all containers including its volumes use:

```
docker rm -f $(docker ps -aq)
```

To delete all the images, use:

```
docker rmi -f $(docker images -aq)
```
