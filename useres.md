Creating users in Jenkins
===========================
1 Open the dashboard of jenkins
2 click on manage jenkins
3 click on manage users
4 clcik on create users
5 enter user credentials

Creating roles and assgning
==============================
1 Open the dashboard of jenkins
2 click on manage jenkins
3 click on manage plugins
4 click on role based authorization strategy plugin
5 install it
6 go to dashboard-->manage jenkins
7 click on configure global security
8 check enable security checkbox
9 go to authorization section-->click on role based    strategy  radio button
10 apply-->save
11 go to dashboard of jenkins
12 click on manage jenkins
13 click on manage and assign roles
14 click on mange roles
15 go to global roles and create a role "employee"
16 for this employee in overall give read access
   and in view section give all access
17 go to project roles-->Give the role as developer
   and patter as Dev.* (ie developer role can access
   only those jobs whose name start with Dev)
18 similarly create another role as tester and assign    the pattern as "Test.*"
19 give all permisiinons to developrs and tester
20 apply--save
21 click on assign roles
22 go to global roles and add user1 and user2 
23 check user1 nad user2 as employees
24 go to item roles
25 add user1 and user2
26 check user1 as developer and user2 as tester
27 apply-->save
If we login into jenkins as user1 we can access on the development related jobs and user2 can access only the testing related jobs
