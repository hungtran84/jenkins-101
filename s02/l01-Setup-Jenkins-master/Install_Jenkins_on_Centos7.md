Based on the official Jenkins [guideline](https://www.jenkins.io/doc/book/installing/)
### Install LTS release
```bash
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
sudo yum upgrade
sudo yum install jenkins java-1.8.0-openjdk-devel
sudo systemctl daemon-reload
```
### Change Jenkins port (optional)
```bash
sudo vim /etc/sysconfig/jenkins
JENKINS_PORT="8000"
```

### Start Jenkins service
```bash
sudo systemctl start jenkins
```

### Check the status of Jenkins service
```bash
sudo systemctl status jenkins
```
#### Check the open port of Jenkins service
```bash
netstat -tulpn | grep LISTEN
```
#### Or
```bash
ss -tupln | grep 8000
```


### (Optional - recommended) Install and configure Firewalld
#### Install and enable firewalld
```bash
sudo yum install firewalld
sudo systemctl enable firewalld
sudo systemctl start firewalld
sudo systemctl status firewalld
```

#### Open firewall for Jenkins service
```bash
firewall-cmd --permanent --new-service=jenkins
firewall-cmd --permanent --service=jenkins --set-short="Jenkins ports"
firewall-cmd --permanent --service=jenkins --set-description="Jenkins port exceptions"
firewall-cmd --permanent --service=jenkins --add-port=8080/tcp
firewall-cmd --permanent --add-service=jenkins
firewall-cmd --zone=public --add-service=http --permanent
firewall-cmd --reload
```

### Get initial Admin password
```bash
cat /var/lib/jenkins/secrets/initialAdminPassword
```