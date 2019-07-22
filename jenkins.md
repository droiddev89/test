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

**Create app bots slack**

Add bot navigation to -> https://api.slack.com/apps
        
![Screen Shot 2019-07-22 at 3.37.09 PM.jpg]({{site.baseurl}}/media/Screen Shot 2019-07-22 at 3.37.09 PM.jpg =200x200)


Navigate to -> OAuth & Permissions and add Scope: incoming-webhook, chat:write:bot

![Screen Shot 2019-07-22 at 3.39.31 PM.jpg]({{site.baseurl}}/media/Screen Shot 2019-07-22 at 3.39.31 PM.jpg)
![Screen Shot 2019-07-22 at 3.39.49 PM.jpg]({{site.baseurl}}/media/Screen Shot 2019-07-22 at 3.39.49 PM.jpg)



Navigate to -> Bot User
		Create bot user
	+ Navigate to -> Installed App Settings
		Click to install app
	+ Add app to channel
		Click to channel -> Channel info -> Add app -> Select app
