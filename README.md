# devops
roadmap to devops

# Table of Contents

1 Jenkins
  
  * [Install Jenkins Master Server](https://github.com/jawad1989/devops/tree/master/Jenkins)
  * Pipelines and Jobs
    * Creating your first Pipeline - with apache Maven
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
2. GitLab
  * Configure Git on Ubuntu
  * GitLab WebHooks
  * GitLab Runners
  

# Devops Project

## 1. GitLab Web Hooks and deploying docker images using Jenkins
Create a web hook in GITLAB, once code is pushed by developer it will run a Jenkins Job. Which will pull the code from GitLab Repository and first deploy the code local workspave, prepare the docker iamge by pulling it from Docker Hub and then running the code on a UAT Server(slave-1). Once the build is successfull another job will run and perform all the steps for deploying the container and code in production server(slave-2) 

**Tools/Tehnolgies Used**
1. AWS
2. GitLab
3. Jenkins
4. Docker Engine
5. Docker Hub
