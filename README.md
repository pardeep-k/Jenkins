
# Jenkins Continues Integration 

Jenkins is a free and open source automation server. Jenkins helps to automate the non-human part of the software development process, with continuous integration and facilitating technical aspects of continuous delivery. It is a server-based system that runs in servlet containers such as Apache Tomcat

## Installation

First, we need to install  [jenkins](https://www.digitalocean.com/community/tutorials/how-to-install-jenkins-on-ubuntu-18-04) follow the link to read article.

# Step 1 — Installing Jenkins
The version of Jenkins included with the default Ubuntu packages is often behind the latest available version from the project itself. To take advantage of the latest fixes and features, you can use the project-maintained packages to install Jenkins.

First, add the repository key to the system:

```bash
$ wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
```
When the key is added, the system will return OK. Next, append the Debian package repository address to the server’s sources.list:

```bash
$ sudo sh -c "echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list"
```
When both of these are in place, run update so that apt will use the new repository:

```bash
$ sudo apt update
```

Finally, install Jenkins and its dependencies:

```bash
$ sudo apt install jenkins
```

# Step 2 — Starting Jenkins
Let’s start Jenkins using systemctl:

```bash
sudo systemctl start jenkins
```

Since systemctl doesn’t display output, you can use its status command to verify that Jenkins started successfully:

```bash
sudo systemctl status jenkins
```

If everything went well, the beginning of the output should show that the service is active and configured to start at boot:

```output
jenkins.service - LSB: Start Jenkins at boot time
   Loaded: loaded (/etc/init.d/jenkins; generated)
   Active: active (exited) since Mon 2018-07-09 17:22:08 UTC; 6min ago
     Docs: man:systemd-sysv-generator(8)
    Tasks: 0 (limit: 1153)
   CGroup: /system.slice/jenkins.service
```
Now that Jenkins is running, let’s adjust our firewall rules so that we can reach it from a web browser to complete the initial setup.

# Step 3 — Opening the Firewall
By default, Jenkins runs on port 8080, so let’s open that port using ufw:

```bash
sudo ufw allow 8080
```

Check ufw’s status to confirm the new rules:
```bash
sudo ufw status
```
You will see that traffic is allowed to port 8080 from anywhere:

```output
Output
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere
8080                       ALLOW       Anywhere
OpenSSH (v6)               ALLOW       Anywhere (v6)
8080 (v6)                  ALLOW       Anywhere (v6)
```

Note: If the firewall is inactive, the following commands will allow OpenSSH and enable the firewall:

```bash
sudo ufw allow OpenSSH
sudo ufw enable
```


Please make sure to update the tests as appropriate.

## Jenkins Installation has been completed now we need to  add jobs

[Full Article](https://dzone.com/articles/learn-how-to-setup-a-cicd-pipeline-from-scratch)

### Hands-On: Building a CI/CD Pipeline Using Docker and Jenkins

**Step 1:** Open your terminal in your VM. Start Jenkins and Docker using these commands:

**Note:** Use sudo before the commands if it displays a "privileges error."

```bash 
systemctl start jenkins 

systemctl enable jenkins 

```



![GitHub Logo](https://www.edureka.co/blog/content/ver.1531719070/uploads/2018/07/CI-CD-Pipeline-Hands-on-CI-CD-Pipeline-edureka-0-1.png)


**Step 2:** Open Jenkins on your specified port. Click on New Item to create a Job.

![GitHub Logo](https://www.edureka.co/blog/content/ver.1531719070/uploads/2018/07/CI-CD-Pipeline-Hands-on-CI-CD-Pipeline-edureka-1.png)


**Step 3:** Select a freestyle project and provide the item name (here I have given Job1) and click OK.

![GitHub Logo](https://www.edureka.co/blog/content/ver.1531719070/uploads/2018/07/CI-CD-Pipeline-Hands-on-CI-CD-Pipeline-edureka-2.png)

**Step 4:** Select Source Code Management and provide the Git repository. Click on Apply and Save button.

![GitHub Logo](https://www.edureka.co/blog/content/ver.1531719070/uploads/2018/07/CI-CD-Pipeline-Hands-on-CI-CD-Pipeline-edureka-3.png
)

**Step 5**: Then click on Build->Select Execute Shell. 


![GitHub Logo](https://www.edureka.co/blog/content/ver.1531719070/uploads/2018/07/CI-CD-Pipeline-Hands-on-CI-CD-Pipeline-edureka-4.png
)


**Step 6:** Provide the shell commands. Here, it will build the archive file to get a war file. After that, it will get the code that is already pulled and then it uses maven to install the package. It simply installs the dependencies and compiles the application.

![GitHub Logo](https://www.edureka.co/blog/content/ver.1531719070/uploads/2018/07/CI-CD-Pipeline-Hands-on-CI-CD-Pipeline-edureka-5.png
)


# Integration Of Jenkins With AWS EC2 Instance Using SSH Plugin 


1. Pre-requisites
2. One Up & Running AWS – EC2 Instance 
3. One UP  & Running Jenkins Server
4. AWS EC2 Public IP Address
5. AWS EC2 Pem File


### Step 1
* Go to: Jenkins -> Manage Jenkins -> Manage Plugins -> Available Tab
* Search For ‘SSH Plugin‘
* Download and Install that Plugin

### Step 2
* Go to: Jenkins -> Manage Jenkins -> Configure System

Now “SSH remote hosts” option will appear on this page.

![GitHub Logo](https://secureservercdn.net/198.71.233.197/a9j.9a0.myftpupload.com/wp-content/uploads/2018/01/Screen-Shot-2018-01-29-at-8.09.42-PM.png
)

* “Add” button will appear in the SSH remote hosts section.
* This plugin can connect multiple EC2 Instances.
* Add button will ask for a number of parameters as described in the image above.


## Parameter Values
* Hostname: Public IP of EC2 Instance or any Domain name of EC2 Instance
* Port: 22 ‘Because 22 Port is for SSH Connections’
* pty, serverAliveInterval, timeout: put the value as described in above image
* Need to Add Credentials by clicking Add button next to Credentials Drop Down.

###  Step 3 
![GitHub Logo](https://secureservercdn.net/198.71.233.197/a9j.9a0.myftpupload.com/wp-content/uploads/2018/01/Screen-Shot-2018-01-29-at-8.23.04-PM.png)
* Add Credentials Popup will appear as explained in the image above.

## Parameter Values
* Kind: SSH Username with Private Key
* Scope: Global
* Username: ec2-user ‘or Any Username of your AWS EC2 Instance’
* Private Key: Select ‘Enter directly’.Here we will add Pem file 
   * Key: Open Pem file with text -> Copy Content -> Paste here.

* Passphrase: leave it blank
ID: leave it blank
Description: Put any Name for your Connection.


### Step 4
* Back to SSH remote hosts in Manage Jenkins -> Configure System.
* Select the credentials that you created recently.
* Then hit ‘Check Connection’ Button.

![GitHub Logo](https://secureservercdn.net/198.71.233.197/a9j.9a0.myftpupload.com/wp-content/uploads/2018/01/Screen-Shot-2018-01-29-at-8.33.39-PM-2.png)


## Congratulations! You successfully Integrated Jenkins with AWS EC2 using SSH remote host.

# Setup settings to listen webhooks on local server

Have you ever tried adding GitHub webhook in Jenkins? In this blog, I will be demonstrating the easiest way to add a webhook in your pipeline.

First, what is a webhook? The concept of a webhook is simple. A webhook is an HTTP callback, an HTTP POST that occurs when something happens through a simple event-notification via HTTP POST.

GitHub webhooks in Jenkins are used to trigger the build whenever a developer commits something to the master branch.

Let’s see how to add build a webhook in GitHub and then add this webhook in Jenkins.

1. Go to your project repository.
2. Go to "settings" in the right corner.
3. Click on "webhooks."
4. Click "Add webhooks."
5. Write the Payload URL as

```bash 

https://228b9f82.ngrok.io/github-webhook/ 
```
```bash
 ngrok http 8080 
```


After this, we need to set up webhook URL to bitbucket / GitHub repository

**Settings > Webhooks**



## Shell Script 

### (Pre Script )Before SSH

```shall
npm install
protractor e2e/protractor.conf.js
```
### (Post Script) After SSH Connection 
```shall
cd /var/www/html/scholarbees-fe/ && 
sudo git pull origin uat 
&& sudo npm install 
&& sudo npm run build-uat 
&& sudo rm -rf ../dist 
&& sudo mv dist/ ../
```

# angular test cases

https://blog.angulartraining.com/how-to-running-angular-tests-on-continuous-integration-servers-ad492219c08c



# Protector for angular / jenkins
https://medium.com/@cnishina/protractor-in-ci-jenkins-6f5fd3fc06ee
# Protector headless browser
https://www.maniuk.net/2017/10/configure-jenkins-and-xvfb-plugin-on-ubuntu.html
## License
[MIT](https://choosealicense.com/licenses/mit/)




```
NOTE make sure you checked the checkbox for **Execute each line** checkbox

