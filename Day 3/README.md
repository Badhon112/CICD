## Day 3: Jenkins installation Options, Docker Setup and Freestyle Job

Install jenkins in docker

```
$ docker run -d -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home --name jenkins-lts jenkins/jenkins:lts

$ docker exec <container_name> cat /var/jenkins_home/secrets/initialAdminPassword
```
