Installing jenkins on Linux machines
=========================================
1 Go to the jenkins server linux machine(username: vagrant password:vagrant)
2 sudo passwd root
  enter some root password
3 su - root
   enter password for root
  
4 Uninstall existing versions of java
   apt-get purge java*

5 Add java8 to the apt-repository
   add-apt-repository ppa:webupd8team/java
 
6 Update the apt repository
   apt-get update

7 Install oracle-java8
   apt-get install oracle-java8-installer

8 Download jenkins keys and add to apt keys
   wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -

  echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list

9 update apt repository
   apt-get update

10 install jenkins
   apt-get install jenkins

11 Install maven and git
   apt-get install maven git


Install Java (Jenkins needs Java 11 or 17):
==============================================

Ubuntu / Debian:
------------------

    sudo apt update
    sudo apt install openjdk-17-jdk -y
    java -version

RHEL / CentOS / Amazon Linux:
--------------------------------

    sudo yum install java-17-openjdk -y
    java -version

🔹 Install Jenkins on Ubuntu / Debian:
=========================================
Step 1: Add Jenkins Repository & Key
    curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
     /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

Step 2: Install Jenkins:
------------------------
    sudo apt update
    sudo apt install jenkins -y

Step 3: Start & Enable Jenkins:
---------------------------------
    sudo systemctl start jenkins
    sudo systemctl enable jenkins
    sudo systemctl status jenkins

Step 4: Open Jenkins in Browser:
------------------------------
http://<server-ip>:8080 (or http://localhost:8080)

Step 5: Unlock Jenkins:
-------------------------
    sudo cat /var/lib/jenkins/secrets/initialAdminPassword
    Copy the password → paste in browser.

Step 6: Finish Setup:
-----------------------
    Install Suggested Plugins
    Create Admin User

Jenkins Dashboard opens 🎉

Install Jenkins on RHEL / CentOS / Amazon Linux:
===============================================
Step 1: Add Jenkins Repo:
--------------------------
    sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo

    sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

Step 2: Install Jenkins:
--------------------------
    sudo yum install jenkins -y

Step 3: Start Jenkins:
------------------------
    sudo systemctl start jenkins
    sudo systemctl enable jenkins

Firewall (Important)

If firewall is enabled:

sudo ufw allow 8080


or

sudo firewall-cmd --permanent --add-port=8080/tcp
sudo firewall-cmd --reload

🔹 Jenkins Lifecycle After Install
Code Push → Jenkins Trigger → Build → Test → Package → Deploy

🔹 Verify Jenkins
ps -ef | grep jenkins


