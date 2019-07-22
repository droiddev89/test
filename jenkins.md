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
    
Start Jenkins

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

**1. Slack notification**

**a. Create app bots slack**

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

**b. Add bot to Jenkins**

Install slack notification plugin
	
    Manage Jenkins -> Manage Plugin -> [select Availble tab] -> search "Slack notification"
	
Add credentials:  Navigation to Manage Jenkins -> Configure System -> Global Slack Notifier Settings
	
    
	Is Bot User? -> clicked
	Integration Token Credential ID -> Add new credentials
		- Domain -> Global credentials (unrestricted)
		- Kind -> Secret text
		- Scope -> Global (Jenkins, nodes, items, all child items, etc)
		- Secret -> [https://api.slack.com/apps -> select app -> OAuth & Permissions -> copy "Bot User OAuth Access Token" paste here]
		- Description -> Name of this configuration

	Channel or Slack ID -> [copy channel id / Channel name] -> Test connection -> make sure channel received message from bots
	Save configuration

![Screen Shot 2019-07-22 at 4.31.50 PM.jpg]({{site.baseurl}}/media/Screen Shot 2019-07-22 at 4.31.50 PM.jpg)

**2. Docker plugin**

Install plugin
		
	Manage Jenkins -> Manage Plugin -> [select Availble tab] -> search "Docker"

Add user jenkins to docker group

	sudo usermod -a -G docker jenkins
	restart jenkins
    
Config Jenkins: Navigation to Manage Jenkins -> Configure System -> Cloud

![Screen Shot 2019-07-22 at 4.17.47 PM.jpg]({{site.baseurl}}/media/Screen Shot 2019-07-22 at 4.17.47 PM.jpg)

![Screen Shot 2019-07-22 at 4.27.45 PM.jpg]({{site.baseurl}}/media/Screen Shot 2019-07-22 at 4.27.45 PM.jpg)

![Screen Shot 2019-07-22 at 4.19.23 PM.jpg]({{site.baseurl}}/media/Screen Shot 2019-07-22 at 4.19.23 PM.jpg)

![Screen Shot 2019-07-22 at 4.20.05 PM.jpg]({{site.baseurl}}/media/Screen Shot 2019-07-22 at 4.20.05 PM.jpg)

## C. SETUP PROJECT

