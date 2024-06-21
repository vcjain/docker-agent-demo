# Setup Docker as Slave Agent

1. Install Docker Plugin in Jenkins
2. Navigate to Manage Jenkins-- Cloud
3. Add Cloud of type Docker
4. Setup Cloud Details
5. Docker Host URI - tcp://IP-ADDRESS-SLAVE:2375
6. Enabled - Check checkbox
7. Expose Docker Host - Check checkbox
8. Container Cap - Change value to your choice lets say 10

9. Add Docker Agent Template
10. Label - Specify label as 'docker-slave'
11. Check the checkbox Enabled
12. Name- Spceify same as label
13. Docker Image - avinashmahto/docker-slave
14. Remote File System Root - /home/ubuntu
15. Connect Method - Connect By SSH
16. SSH Key - Use Configured SSH Credentials
17. Add a Credentials as Username and password as jenkins/jenkins
18. Host Key Verification - Non veriftying Verication strategy
19. Apply and Save 
