
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

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

# Jenkins Installation has been completed now we need to  add jobs


## License
[MIT](https://choosealicense.com/licenses/mit/)
