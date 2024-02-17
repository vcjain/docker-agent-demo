# Jenkins Distributed Architecture Setup

## Provision VM

- Provision 2 Ec2 instance on AWS. One instance will be used for Java Agent and another for ssh connection
- While launching instance ensure to define public-private key



## Configuring Jenkins
- Navigate to ManageJenkins--> Security--> Agent
- Enable TCP port for inbound agents
- Select Fixed, and give port value as 50000
- Install plugin Docker and Docker Pipeline

## Adding Node as Java Agent
- Naivate to ManageJenkins--> Node
- Choose Type as Permanent Agent and click Create
- Follow instruction and Save 
- - Define label of your choice like ssh
- - Remote Dir as /home/ubuntu
- - Lanuch Method - Connecting by controller
- On Node page, click on Agent name, it will display some commands. We will need to run these command on Agent terminal

 ### Connecting Slave with Master
  - Update package 
  - Install Java
  - Run command displayed on master node page
  - keep the process running, so not terminate process

## Adding Node using SSH
- Naivate to ManageJenkins--> Node
- Choose Type as Permanent Agent and click Create
- Follow instruction and Save 
- - Define label of your choice like ssh
- - Remote Dir as /home/ubuntu
- - Lanuch Method - via ssh
- - Add host and credentials, private key for slave node
- - Select 'Non verifying' in Host key verification
- On Node page, check the status, you can relauch and check logs

## Running Docker container

- Install docker on a slave machine. Follow instruction from below url
- https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-22-04
- Relaunch Instance

## Docker Hub Account
- Open hub.docker.com
- Signup/login on hub.docker.com

### Jenkins steps
- Install Docker Pipeline plugin in Jenkins
- Create a credentials "dockerhub" (username and password) for hub.docker.com

----

<br>
<br>
# Usages

- Launch pipeline using Jenkinsfile for basic Java application on a agent with Java already installed
- Launch pipeline using Jenkinsfile-docker for using agent as docker with image
- Launch pipeline using Jenkinsfile-dockerfile for using agent as docker with dockerfile kept in the repo along with Jenkinsfile
