
# Configure Docker Cloud in Jenkins

This guide explains how to configure **Docker Cloud** in Jenkins to dynamically provision build agents using Docker containers.

---

## Prerequisites

- Jenkins is installed and running
- Docker is installed on the Jenkins host machine
- Docker plugin is installed in Jenkins
- Jenkins has administrative access

---

## Steps to Configure Docker Cloud

### 1. Open Jenkins Docker Cloud Configuration

Navigate to:


Manage Jenkins → Manage Nodes and Clouds → Configure Clouds


---

### 2. Add a New Docker Cloud

- Click **"Add a new cloud"**
- Select **"Docker"**

---

### 3. Set Docker Host URI

- For **local Docker daemon** (running on same host as Jenkins):

```

unix:///var/run/docker.sock

```

- For **remote Docker host**:

```

tcp\://\<DOCKER\_HOST>:2375

```

---

### 4. For SimpliLearn Lab (Using Local Docker)

If you're using Jenkins in the **SimpliLearn lab environment**, Docker runs locally. You must allow the Jenkins user to access the Docker socket.

Run the following commands:

```bash
sudo usermod -aG docker jenkins
```
```
sudo systemctl restart jenkins
````

> Note: Restarting Jenkins is required for the new group permissions to take effect.

---

### 5. Validate Connection

* Click the **"Test Connection"** button
* You should see a confirmation that the Docker host connection is successful

---

## Next Steps: Add Docker Agent Template

Once the Docker Cloud is configured, you can define a Docker Agent Template:

* **Label**: (e.g., `docker-agent`)
* **Name**: docker-agent
* **Enabled**: Check the checkbox
* **Docker Image**: Use a prebuilt agent image (e.g., `jenkins/inbound-agent`)
* **Remote File System Root**: (e.g., `/home/jenkins`)
* **Usage**: Use this node as much as possible
* **Connect Method**: Attach Docker as Container, Levave everything (user, Java, EntryPoint CMD) as empty.

Use this label in your Jenkins pipelines to run builds inside Docker containers.

---

Run Pipeline to verify configuration

```
pipeline {
  agent 
	{
        label 'docker-agent'
    }
    stages{
        stage('checkout'){
            steps{
                checkout poll: false, scm: scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/vcjain/docker-agent-demo.git']])
            }    
        }
    }
}
```

