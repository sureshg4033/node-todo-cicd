# node-todo-cicd

Launch an EC2 instance on AWS with an Amazon Linux 2 AMI.

Connect to your EC2 instance using SSH.

Install Docker on your EC2 instance by running the following commands:

sudo yum update -y
sudo apt-get  install docker
sudo service docker start
sudo usermod -a -G docker ec2-user

Install Java on your system. You can download and install the latest version of Java from the official Java website.

  sudo yum install java-1.8.0-openjdk -y

Install Jenkins on your system. You can download and install the latest version of Jenkins from the official Jenkins website.

Once Jenkins is installed, navigate to the Jenkins dashboard in your web browser and create a new job. Give the job a name and select "Pipeline" as the job type.

Under "Pipeline", select "Pipeline script" and paste the following script:

  pipeline{
      agent any
      stages{
          stage('code clone'){
              steps{
                  git url:'https://github.com/dhiyani12/node-todo-cicd.git', branch: 'master'
              }
          }
          stage('build' ){
              steps{
                sh 'docker build . -t django-todo-app'
              }
          }
         stage('deploy'){
              steps{
                sh 'docker-compose down && docker-compose up -d'
  }
  }
  }
  }

This script will perform the following steps:

It will clone your repo

It will build image from the Dockerfile

Start the application using Docker Compose.

Save the job and navigate to the job's configuration page. Under "Build triggers", select "GitHub hook trigger for GITScm polling". This will enable Jenkins to automatically trigger the pipeline whenever changes are pushed to the GitHub repository.

Next, create a webhook on your GitHub repository. Navigate to the repository's settings page, select "Webhooks", and create a new webhook. Set the payload URL to http://<jenkins-host>:<jenkins-port>/github-webhook/, replacing <jenkins-host> and <jenkins-port> with the hostname and port of your Jenkins server.

Create a docker-compose.yml file in the root directory of your project, with the following contents:

version: '3.9'

services:
  web:
    build: .
    ports:
      - "8000:8000"

This file defines a Docker Compose service for your application, with the image name node-todo-cicd, and maps port 8000 on the host to port 8000 in the container.

Commit your changes to your GitHub repository, and wait for Jenkins to automatically trigger the pipeline. You should see the pipeline stages running in the Jenkins console output.

Once the pipeline has completed successfully, your application should be deployed and accessible at http://<publicip>:8000/.

That's it! You now have a fully automated CI/CD pipeline for your Node.js application, using Docker, Java, and Jenkins.
