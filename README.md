# Jenkins-Tutorial:
=====================

Installing jenkins on Windows
================================
Jdk install:
-----------
1 Download and install Java (JDK 11 or 17 required)
2.https://www.oracle.com/in/java/technologies/downloads/#jdk25-windows
3.install it
4.Set JAVA_HOME:
    JAVA_HOME = C:\Program Files\Java\jdk-17
5.Add to PATH:
%JAVA_HOME%\bin
6. Above 4 and 5 points added in enviroment varaible in your local mechine
java -version

Step 1: Download Jenkins:
============================
    a. Go to https://www.jenkins.io/download/
    b. Click Windows → Download Jenkins.msi

Step 2: Install Jenkins:
========================
    1.Double-click jenkins.msi
    2 .Click Next
    3.Choose install path (default is fine)
    4 .Jenkins installs as a Windows Service
    5.Finish installation 

Step 3: Start Jenkins:
=====================
    1.Jenkins starts automatically
    2.Open browser and go to:
    3.http://localhost:8080

 Step 4: Unlock Jenkins:
 ========================
    1.Jenkins asks for initial admin password
    2.Open this file:
       a. C:\Program Files\Jenkins\secrets\initialAdminPassword
    3.Copy the password and paste it into the browser

 Step 5: Install Plugins:
============================
    1.Click Install suggested plugins
    2.Wait until installation completes

Step 6: Create Admin User:
===========================
    1.Create username & password
    2.Save and continue
    3.Jenkins dashboard opens 🎉
Verify Jenkins Service

Open Services (services.msc)
Check:

Jenkins → Running

