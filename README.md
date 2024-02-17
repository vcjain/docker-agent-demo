# Jenkins Distributed Architecture Setup

## Provision VM

- Provision 2 Ec2 instance on AWS. One instance will be used for Java Agent and another for ssh connection
- While launching instance ensure to define public-private key



## Configuring Jenkins
```
- Navigate to ManageJenkins--> Security--> Agent
- Enable TCP port for inbound agents
- Select Fixed, and give port value as 50000
- Install plugin Docker and Docker Pipeline
- Update security group to allow all TCP port for training on Jenkins master
```

There are different method that we can use to add a Node as a Slave to Jenkins
1. Using Java Agent
2. Using ssh connection
3. Docker container as slaves
4. Using Cloud Platform for OnDemand machines


## Adding Node as Java Agent
We can connect a Node as Slave using JNLP. In this method a Jaba agent is executed on the Slave node, which will listen for any command from 
, master node and it will execute them on the slave machine.
It is important for a slave node to run Java agent continusely, otherwise slave connection will break.

```
ON Slave Machine,
- Update package & Install Java on slave node
```

```
On Jenkins console
- Naivate to ManageJenkins--> Node
- Choose Type as Permanent Agent and click Create
- Follow instruction and Save 
- - Define label of your choice like ssh
- - Remote Dir as /home/ubuntu
- - Lanuch Method - Connecting by controller
- On Node page, click on Agent name, it will display some commands. We will need to run these command on Agent terminal
```
 ### Connecting Slave with Master
 ```
ON Slave Node
  - Run command displayed on master node page
  - keep the process running, so not terminate process
```


## Adding Node using SSH
We can also add a Node as a Jenkins Slave using ssh. In this method, we do not need to run a Java Agent on slave machine, rather master node will
connect using ssh just like we are connecting to any EC2 machine using public and private key. 

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
As the world is moving to docker container, as third method and most recent method to run slave as docker container. We will need to have machine
with Docker installed on it. This node will be used as Docker Host. When we run a Job, a conatiner will be created, excuted Job and will terminate it.
With this method, we can optimally use our resources.
```
- Install docker on a slave machine. Follow instruction from below url
- https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-22-04
- Relaunch Instance
```
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
