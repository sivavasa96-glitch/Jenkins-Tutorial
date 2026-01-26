For passwordless ssh
=========================
1 Go to jenkins server 
2 when we install jenkins a user called jenkins
  gets created.we should swithc into this user   account
  sudo su - jenkins
3 ssh-keygen
  This will generate 2 keys public key and private     key.The public key should be copied into QAServer 
  and prodserver
4 ssh-copy-id vagrant@ipaddress_of_QAServer
  ssh-copy-id vagrant@ipaddress_of_ProdServer

5 Go to the dashboard of jenkins
6 goto the Dev_01 job created-->Click on configure
7  go to pipeline section-->Pipeline syntax
8 we should downlaod the testing code from git
  and run a jar file which is present in the repo
9 select git-->Specify the url of the testing github
  repository
10 click on generate pipelins script
11 copy this script into jenkinsfile
12 to run the jar file to executing the automation    testing programs
13 clcik on pipelinesyntax-->Select sh:shell
14 java -jar path_of_jar file
15 click on generate pipelins script
16 copy the groovy script and paste in jenkins file
17 To deploy the war file in prod env repeat the scp
   command with production url


Staging in pipelins scripts
A single pipeline can containe multiple stages
a stage can contain multiple steps

Every individual action performed by jenkisn can be called as a stage
Syntax
stage('label for stage')
{

}

//Sample docker file

node('master')
{
    git 'https://github.com/selenium-saikrishna/maven.git'

    sh '''mvn clean
        mvn package'''
   
   sh 'scp /var/lib/jenkins/workspace/Dev_01/webapp/target/webapp.war vagrant@192.168.61.22:/var/lib/tomcat7/webapps/qaenv.war'
   
   git 'https://github.com/selenium-saikrishna/testing.git'
   
  sh '''java -jar 
   target/testing1.jar'''
   
    sh 'java -jar /var/lib/jenkins/workspace/Dev_01/target/testing1.jar'
   
   
   
   
sh 'scp /var/lib/jenkins/workspace/Dev_01/webapp/target/webapp.war vagrant@192.168.61.13:/var/lib/tomcat7/webapps/prodenv.war'
   
   
}

BlueOcean UI
==================
This is a new user interface of Jenkins with more 
graphical content
To install blue ocean
1 Open the dashboard of jenkins
2 Click on manage jenkins-->manage plugins
3 go to available section-->Search for blue ocean
4 Install it
5 Restart jenkins
