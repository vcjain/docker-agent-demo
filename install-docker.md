# Docker Installation on Ubuntu 22.04

First, update your existing list of packages
```
sudo apt-get update
```
Next, install a few prerequisite packages which let apt use packages over HTTPS:
```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```
Then add the GPG key for the official Docker repository to your system:

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
Add the Docker repository to APT sources:
```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
Update your existing list of packages again for the addition to be recognized:
```
sudo apt-get update
```
Make sure you are about to install from the Docker repo instead of the default Ubuntu repo:
```
apt-cache policy docker-ce
```
Finally, install Docker:
```
sudo apt install docker-ce -y
```
Docker should now be installed, the daemon started, and the process enabled to start on boot. Check that it’s running:
```
sudo systemctl status docker
```

## Run without sudo
If you want to avoid typing sudo whenever you run the docker command, add your username to the docker group:
```
sudo usermod -aG docker ${USER}
```

Close the EC2 terminal window and open a new terminal window. Now you should be able to access docker command without sudo.

```
docker ps
```

## Open remote connection on the Docker Host
Open the docker service file 
```
sudo systemctl edit docker.service
```
Please add your values between first line and commented line.
```
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -Hunix:// -Htcp://0.0.0.0:2375
```
We should replace the 0.0.0.0 with a valid ip address if you restrict it to only a machine

```
sudo systemctl daemon-reload
```
```
sudo systemctl restart docker
```
```
sudo systemctl status docker
```


