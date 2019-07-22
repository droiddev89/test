## A. INSTALL

Update system

	sudo yum install epel-release
	sudo yum update
	Install Java
    
Install Jenkins
```
    sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
    sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
    yum install jenkins -y
```    
    
Start

	sudo systemctl start jenkins.service
	sudo systemctl enable jenkins.service
    
Firewall

	sudo firewall-cmd --zone=public --permanent --add-port=8080/tcp
	sudo firewall-cmd --reload
    
Running

	http://<your-server-IP>:8080
  
Config file:

	/etc/sysconfig/jenkins
    
Find all xml config file

	find / -name "config.xml" | grep "jenkins"

## B. CONFIG PLUGIN & SYSTEM

**1. Create app bots slack**

Add bot navigation to 

	https://api.slack.com/apps

Navigate to -> OAuth & Permissions and add Scope: 
	
    + incoming-webhook
    + chat:write:bot

Navigate to -> Bot User

	+ Display name
    
    + Default username
    
    -> Save Change
    
    
    
Navigate to -> Installed App Settings

	Click to install app

Add app to channel
		
	Click to channel -> Channel info -> Add app -> Select app
