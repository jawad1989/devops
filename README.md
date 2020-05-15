# devops
roadmap to devops


* Creating a CICD Solution
* [Install Jenkins Master Server](https://github.com/jawad1989/devops/tree/master/Jenkins)
* Free Style Job: Running Docker Containers
* Free Style Job Running Java Code
* How to create a remote build in Jenkins
* Create Job Chaining in Jenkins
* Create and Configure Jenkins Slave Nodes using SSH 
  * Creating public/private keys
  * configuring slave machine on jenkins master UI
* Automated deployment pipeline
  * Deploying War file in Tomcat Server
* Configure Git on Ubuntu
* Jenkins Creating/managing Users
* Jenkings Creating API Token for GIT
* Install Plugins in Jenkins 
  * GITLAB
  * Deploy to container
  * Blue ocean
  * Blue ocean
* GitLab WebHooks
* GitLab Runners
* Creating your first Pipeline - with apache Maven
* Multi Branch Pipeline: Checks the repository for any new change in branch, if a change exists, it will run the JenkinsFile and run the pipeline.
* How to Create Parameterized Jenkins Job

Devops Project
Create a web hook in GITLAB, once code is pushed by developer it will run a Jenkins Job. Which will pull the code from GitLab Repository and first deploy the code local workspave, prepare the docker iamge by pulling it from Docker Hub and then running the code on a UAT Server(slave-1). Once the build is successfull another job will run and perform all the steps for deploying the container and code in production server(slave-2) 
