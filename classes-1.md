Introduction for Jenkins:
=========================

what is jenkins:
=================

Jenkins is an open-source automation tool mainly used in DevOps to build, test, and deploy applications automatically.

What Jenkins does:
======================

    1. Automatically pulls code from Git (GitHub, GitLab, Bitbucket)
    2. Builds the application (Maven, Gradle, npm, etc.)
    3. Runs tests (unit, integration, automation)
    4. Deploys the app to servers, Docker, Kubernetes, cloud, etc.
    5. Sends build status (success/failure) notifications

Why Jenkins is used:
=====================

    1.Supports CI/CD (Continuous Integration & Continuous Deployment)
    2.Detects bugs early
    3.Saves time and reduces human errors
    4.Huge plugin support (Git, Maven, Docker, Kubernetes, SonarQube)

Real-world example:
========================

    Developer pushes code → Jenkins auto builds → tests → creates JAR/WAR → deploys → done 🚀

Lifecycle in Jenkins Pipeline stages::
======================================

Checkout → Build → Test → Analyze → Package → Deploy → Monitor

1.Code Commit
-------------

    Developer writes code and pushes it to Git (GitHub/GitLab/Bitbucket).

2.Trigger Jenkins
-----------------

    Jenkins job starts automatically (via webhook, SCM poll, or manual trigger).

3.Checkout Source Code
----------------------

    Jenkins pulls the latest code from the repository.

4.Build
------------

    Code is compiled and packaged (JAR/WAR/Docker image).
    Tools: Maven, Gradle, npm, Docker.

5.Test
------------

    Runs automated tests.
    Unit tests, integration tests, UI tests.

6. Static Code Analysis (Optional)
-----------------------------------

    Code quality and security checks.
    Tools: SonarQube, Checkstyle.

7. Artifact Creation & Storage
-------------------------------

    Build artifacts are created and stored.
    Example: Nexus, Artifactory, Docker Registry.

8.Deploy
-------

    Application is deployed to target environment.
    Dev → QA → Staging → Production
    Tools: Tomcat, Kubernetes, AWS, Azure.

9.Verification
---------------

    Smoke tests / health checks run after deployment.

10.Notification & Feedback
------------------------

    Jenkins sends build status to developers.
    Email, Slack, Teams.

CI-CD Stages
---------------

1 Stage 1 (Continuous Download)
	In this stage Jenkins is integrated with the remote version controlling system(git) in susch a way that when ever developers make changes to the code it will detect those changes and download from the remote repository

2 Stage 2 (Continuous Build)
	The code downloaded in  the previous stage has to be converted into an artifact.This artifact can be in the form of a jar,war,ear,exe file.This process is called as the build process and Jenkins will perform this step with the help of plugins like ant,maven,ms build etc

3 Stage 3 (Continuous Deployment)
	The artifact created in the previous stage has to e deployed into QA servers.The testing servers might be running on application servers like tomcat,jboss weblogic etc.The artifact has to deployed into these servers where testers can access and test the application

4 Stage 4 (Continuous Testing)
	The testers will prepare some automation testing programs using tools like selenium, tosca,codedui etc.These testing programs
will be uploaded by the testers into the git version controlling system.Jenkins should download these programs and run them on the application that was deployed into the testing servers.If testing fails jenkins will send automated notifiactions to the team memebers and developers should fix the defects and upload the modified code into the git repository.Jenkins will again trigger the above 4 steps

5 Stage 5 (Continuous Delivery)
	If testing passes then jenkins will deploy the artifact into the production servers after taking approvals from the team members.Once it is deployed into the prod servers the enduser/client can start accessing it.

Note: The first four stages are called Continuous Integration and the fifth stage is called continuous delivery

Stage 1 (Continuous Download)
------------------------------

1 Open the dashboard of jenkins(localhost:8080)
2 Click on New item
3 Enter item name as "Development"
4 Click on Free style project
5 Click on Ok
6 Go to Source code management
7 Select Git
8 Enter the github url where developers have uploaded the code
  https://github.com/selenium-saikrishna/maven.git
9 Click on Apply--->save
10 Go to the dashboard of jenkins
11 Go to the Development job--->click on Build icon
	The above job will download all the code uploaded by 
the developer into the github repository.


Setting the path of maven in jenkins
--------------------------------------

1 Open https://maven.apache.org/download.cgi
2 Go to Files section on this page and download th bin.zip    version.
3 Extract it and open it and copy its path
4 Open the dashboard of jenkins
5 Click on manage jenkins
6 Click on Global tool configurations
7 Go to Maven installations
8 Click on Add maven
9 Enter some anme for maven(mymaven)
10 Paste the path of Maven in MAVEN_HOME location
12 Apply--->save


Stage 2 (Continuous Build):
===============================

1 Open the dashboard of jenkins
2 Go to the development job--->click on configure
3 Go to Build section
4 Click on add build step
5 Click on Invoke top level maven targets
6 Select maven as mymaven
7 Enter goal as   package
8 Click on Apply--->save
9 Go to dashboard of jenkins
10 Go to the development job--->click on Build icon
	The above job will now create an artifact from the code that was downloaded in the previous stage.This artifact comes in the format of a war file

Step 3 (Continuous Deployment)
---------------------------------

1 Open the dashboard of jenkins
2 Click on Manage Jenkins-->Manage Plugins
3 Go to Available tab-->Search for "Deploy to   container" plugin
4 Install it
5 Go the dashboard of jenkins
6 Go to the development job we created-->Click on
  configure
7 Go to post build actions-->Click on Add post build   action-->click on deploy war/ear to container
8 Enter tomcat credentilas-->apply-->save

Configuring tomcat
====================

1 Download tomcat 7 from 
  https://tomcat.apache.org/download-70.cgi
2 Extract it and open it-->open the conf folder
  open server.xml file-->Search for "connector port"
  and change the port no from 8080 to 8899
  Open tomcat-users.xml
  add the below statement
  <user username="admin" password="admin"                            roles="manager-script"/>
3 Open the bin folder in tomcat
4 click on startup.bat file

We should be able to access the home page of tomcat
from any browser(localhost:8899)

Step 4 (Continuous Testing):
-------------------------------

1 Open the dashboard of jenkins
2 Click on Newitem-->Give item name as "Testing"
3 Click on Free style project-->ok
4 The testing team will provide the url of github
  where they have uploaded their automation testing programs
5 Go to source code management-->Click on git
6 Enter the github url of the testing project
  https://github.com/selenium-saikrishna/testing.git
7 Click on apply-->save
8 once the testing code is downloaded into jenkins workspace
  in the target we will find a jar file called testing.jar
  this jar file can execute all the testing programs on the
  application deployed into QA env
9 Go to dashboard of jenkins
10 go to the "Testing" job that we created-->click on downward
   arrow-->configure
11 Go to build section-->click on "add build step"
12 click on execute windows batch command
13 java -jar target/testing.jar
14 apply-->Save


Note:To link the development job with the testing job
1 Go to the dashboard of jenkins
2 Go to development job
3 Click on downwar arrow-->configure
4 Go post build actions-->Click on build other   project-->enter project name as testing
5 click on apply-->save

Step 5 (Continuous Delivary):
===============================

We have created2 jobs in jenkins(development,testing)
development has has done the below three activities
1 Downloading the development code from git
2 Creating a war file with the help of maven
3 deploying that war file into the tomcat server
  on qaenvironment
The war file created in step no2 by development job
should be passed to testing job.
This can be done using a plugin called "copy artifact plugin"

1 Open the dashboard of jenkins
2 click on manage jenkins-->manage plugins
3 click on available section--search for copy   artifact plugin and install it
4 Go to the dashboard of jenkins-->go to the   development job-->Go to its configuration page
  go to post build actions-->click on add post build   action-->click on archive the artifacts
  Files to archive----**/*.war
5 apply-->save
6 Go to the dashboard of jenkins-->Go to testing job
7 click on configure-->Go to build section
8 click on add build step-->copy artifacts from   another project
9 enter the project name as Development
10 Apply
11 The war file which has been copied from the
   development job into testing job should be    deployed into tomcat server in prodenv
12 click on post build actions
13 click on add post build actions
14 deploy war/ear to container
15 apply-->save

Setting the path of java,maven and git
--------------------------------------------

1. Open the dashboard of jenkins(192.168.61.11:8080)
2. Click on Manage Jenkins-->Global tool configuration
3. Go to JDK section-->Click on jdk installations-->give some name to java--> paste the pasth of java home
  Note: to find path of java home dir
  a) open the jenkins linux server terminal
  b) which java 
       /usr/bin/java
  c) readlink -f /usr/bin/java
  d) copy the path before bin folder and paste in java_home of jenkins(/usr/lib/jvm/java-8-oracle/jre)

4) Go to git section-->give some name to git-->paste the path of git
   a) which git
       /usr/bin/git(copy this path and paste in git section of jenkins)

5) Go to maven-->Click on maven installations-->give some name to maven--> paste the pasth of maven home
   Note: to find path of maven home dir
  a) open the jenkins linux server terminal
  b) which mvn 
       /usr/bin/mvn
  c) readlink -f /usr/bin/mvn
  d)copy the path before bin folder and paste in          maven_home of jenkins(/usr/share/maven)




