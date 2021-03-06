# devops
roadmap to devops

# Table of Contents
1. Bash
   * [One Liner Commands](https://github.com/jawad1989/devops/blob/master/bash/one-liners/)
   * Installing Packages i.e. (Java,MVN,GIT etc)
   
2. Jenkins
    * [Install Jenkins Master Server](https://github.com/jawad1989/devops/tree/master/Jenkins)
    * Pipelines and Jobs
      * Creating your first Pipeline - with apache Maven
      * Creating Pipeline as Code - Jenkinsfile on Git
      * Free Style Job: Running Docker Containers
      * Free Style Job Running Java Code
      * How to Trigger a remote build in Jenkins
      * Create Job Chaining in Jenkins
      * Multi Branch Pipeline:
      * How to Create Parameterized Jenkins Job
      * Automated deployment pipeline
        * Deploying War file in Tomcat Server
      * Create and Configure Jenkins Slave Nodes using SSH 
      * Jenkins Creating/managing Users
    * Jenkings Creating API Token for GIT
    * Install Plugins in Jenkins 
      * GITLAB
      * Deploy to container
      * Blue ocean
      * Pipeline Build View
    * Updating Jenkins to Newer Version
    
3. GitLab
    * Configure Git on Ubuntu
    * GitLab WebHooks
    * GitLab Runners
    * GIT
       * Branching
       * Stash
  
4. Docker
    * Creating a Volume 
    * Sharing App on docker hub
    * Run hello world Container
    * Create a HTTPD Server
    * Create Container and deploy Static Website
    * Installing Jenkins as Service
    * Installing Node.js on dockers
    * Installing Tomcat on on Docker
5. Kubernetes
    * Create a deployment
    * Minikube
      * Install Minikube and Kubectl
      * Launch Single Node Cluster
      * Manage your Cluster
      * Kuberets Dashboard
      * Rolling Updates
      * Scaling Your App
6. Docker Swarm
    * installing Service
    * Adding Slave Nodes
    * Installing Portainer for Docker Swarm Management
7. Virtual Box
    * install ubuntu from ISO
    * Install ubuntu from VID
    * Creating Static IP for VM
    * Resizing a Harddish - Ubuntu Guest and Windows Host
8. AWS Cloud
    * Launching EC2
    * Connectin EC2 with SSH and generating key pair
9. Azure Cloud
    * Creating Resource Group
    * Create Virtual Network
    * Create VPN Gateway
    * Setup VPN Client
    * Create a Private Network
    * Create a Private NAS
    * Creating VM - ubuntu
    * Setup Public Load Balancer
    * Setup Private Load Balancer
 
    

# Devops Project

## 1. GitLab Web Hooks and deploying docker images using Jenkins
Create a web hook in GITLAB, once code is pushed by developer it will run a Jenkins Job. Which will pull the code from GitLab Repository and first deploy the code local workspave, prepare the docker iamge by pulling it from Docker Hub and then running the code on a UAT Server(slave-1). Once the build is successfull another job will run and perform all the steps for deploying the container and code in production server(slave-2) 

**Tools/Tehnolgies Used**
1. AWS
2. GitLab
3. Jenkins
4. Docker Engine
5. Docker Hub

## 2. SonarQube Integration with Jenkins and Gitlab
Repository is placed at Gitlab, when a Jenkins Job runs it clones the repo from Gitlab, analayzed the code using SonarQube, cleans,runs and packages the maven project and deploys the code at Tomcat Server running on docker

**Techs Used**

* Jenkins
* SonarQube
* PostGress Database
* Gitlab
* Tomcat
* Docker
* AWS EC2

**Steps**

* [Installing PostGress](https://github.com/jawad1989/devops/tree/master/aws/postgress-install)

* [Installing SonarQube](https://github.com/jawad1989/devops/tree/master/sonarqube)

* [Installing Docker Enginer with Tomcat](https://github.com/jawad1989/devops/tree/master/projects/tomcat-docker)

* [Integrating Sonarqube with Jenkins](https://github.com/jawad1989/devops/tree/master/Jenkins/jenkins-sonarqube)
