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

**1. New project, select type: Multibranch Pipeline**

![Screen Shot 2019-07-22 at 4.57.16 PM.jpg]({{site.baseurl}}/media/Screen Shot 2019-07-22 at 4.57.16 PM.jpg)

**2. Config project**

![Screen Shot 2019-07-22 at 5.00.19 PM.jpg]({{site.baseurl}}/media/Screen Shot 2019-07-22 at 5.00.19 PM.jpg)

![Screen Shot 2019-07-22 at 5.00.31 PM.jpg]({{site.baseurl}}/media/Screen Shot 2019-07-22 at 5.00.31 PM.jpg)

![Screen Shot 2019-07-22 at 5.00.44 PM.jpg]({{site.baseurl}}/media/Screen Shot 2019-07-22 at 5.00.44 PM.jpg)

## D. ENABLE PERMISSION ON PROJECT FOR EACH USER

Ref: 
	
    https://www.oodlestechnologies.com/blogs/Project-Role-based-authorization-on-Jenkins/

Add user

	Navigate to Manage Jenkins -> Manage Users -> Create User
    
Enable project base security on system
	
    Navigate to Manage Jenkins -> Configure Global Security
	In "Authorization", Select "Project-based Matrix Authorization Strategy". 
		- Add "Admin" user and check all the checkbox to grant all permission to admin user.
		- Authenticated Users -> check on: Overall [Read]
		- Anonymous Users -> Uncheck all
		- Add new user or group to custom authentication here
        
![Screen Shot 2019-07-22 at 5.55.05 PM.jpg]({{site.baseurl}}/media/Screen Shot 2019-07-22 at 5.55.05 PM.jpg)

Retrict permission of project

	Select project -> Configure
    Enable project-based security
		- Uncheck all default role
		- Add new user or group to custom authentication here




