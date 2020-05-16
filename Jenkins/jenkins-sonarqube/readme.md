## Pre Reqs
* install Jenkins
* Install SonarQube

## install plugins
Once logged in make sure install below plugins
* SonarQube Scanner
* Deploy to Container


### Generate Token

After Logged in. __Goto Administration->Security->Users__

![Token](https://github.com/jawad1989/devops/blob/master/projects/sonarqube-jenkins/image.png)

Enter any Name in Generate Token e.g. __sonarqube_token__
click generate and copy the token

```3ee65a6c6f961ccef39404ca869125d8beddcd18```

![Generate Token](https://github.com/jawad1989/devops/blob/master/projects/sonarqube-jenkins/generate%20token%202.PNG)

### update token in Jenkins

Goto __ManageJenkins->ConfigureSystem__ and add the sonarqube serve details plus the token 

![Add SonarQube](https://github.com/jawad1989/devops/blob/master/projects/sonarqube-jenkins/Configure%20Sonar.PNG)
![Add Token](https://github.com/jawad1989/devops/blob/master/projects/sonarqube-jenkins/Add%20Token.PNG)


### Create a Job

__GIT Repository URL__ :https://github.com/sivajavatechie/JenkinsWar.git
![Add Jenkins_job_a](https://github.com/jawad1989/devops/blob/master/projects/sonarqube-jenkins/sonat%20job-1.PNG)

![Add Jenkins_job_b](https://github.com/jawad1989/devops/blob/master/projects/sonarqube-jenkins/sonat%20job-2.PNG)



### Verify Code analyzed by SonarQube in browser

![Add Jenkins_job_b](https://github.com/jawad1989/devops/blob/master/projects/sonarqube-jenkins/4%20-%20sonar.PNG)

![Add Jenkins_job_b](https://github.com/jawad1989/devops/blob/master/projects/sonarqube-jenkins/5%20-%20sonar.PNG)
