Creating a job in Jenkins
---------------------------
1 Open the dashboard of jenkins(localhost:8080)
2 Click on New item
3 Give some name to item(sample)
4 select Free style project
5 Click on OK
6 Go to build section
7 Click on Add build step-->Execute windows batch   command
   echo "Hello Jenkins"
8 Click on Apply-->Save
9 Go to the dsahboard of jenkins
10  go to the sampke job that we created
11 Click on build icon.

Scheduling the build for a particular date and time
------------------------------------------------
1 Open the dashboard of jenkins
2 Go to the sample job we created
3 click on downward arrow-->Configure
4 Go to build triggers-->Click on build   periodically-->Schedule the date and time
5 click on Apply-->Save


Sending automated email from jenkins
--------------------------------------
1 Open the dashboard of jenkins
2 Go to the sample job we creaated
3 click on downward arrow-->configure
4 Go to post build actions-->Click on add post   build action-->click on email notifications
5 enter email ids of our team memebers seperated
  by a space
6 click on apply-->save
7 goto dashboard of jenkins-->click on Manage    jenkins
8 click on configure system
8 go to "email notification" section
9 SMTP server --- smtp.gmail.com
  click on Advanced
10 check Use SMTP Authtenctication
11 enter your gmail id and password
12 check Use SSL
13 SMTP ---- 465
14 Check "Test configuration by sendinf test    email"
15 Enter your gmail id
16 Click on Test configuration

Setting the path of git in jenkins
-------------------------------------
1 Install git from https://git-scm.com/downloads
2 Open c:-->programs files-->git-->bin
  Copy the path of git.exe
3 Open the dashboard of jenkins
  localhost:8080
4 Click on Managejenkins
5 Click on Global tool configurations
6 Go to Git section
7 enter some name for git
  Paste the path of git
