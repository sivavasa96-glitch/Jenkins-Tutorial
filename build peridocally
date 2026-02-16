✅ 1) Jenkins Job (Project)
What is a Jenkinsjob

“A Jenkins job is basically a task or project that Jenkins runs. A job can be used to build code, run tests, create artifacts, or deploy the application.”

✅ Types of Jenkins Jobs
========================

1) Freestyle Project

“Freestyle is the basic Jenkins job. It is created using the Jenkins UI and we configure steps like Git checkout, build commands, and post-build actions. It’s simple but not best for complex CI/CD.”

2) Pipeline

“Pipeline job is used to create CI/CD using code. We write the stages like build, test, deploy inside a Jenkinsfile. It is better for real-time projects because it is reusable and version controlled.”

3) Multibranch Pipeline

“This job automatically detects branches in Git like main, dev, feature branches. It runs builds separately for each branch if Jenkinsfile is present. It is very useful in real-time projects.”

4) Folder

“Folder is used to organize Jenkins jobs. When there are many jobs, we keep them inside folders like Dev, QA, Prod, or based on teams.”

5) GitHub Organization

“This job is used when we want Jenkins to scan an entire GitHub organization. It automatically finds all repositories and builds them if Jenkinsfile exists.”

✅ 6) Build Triggers:
===================

1) Build periodically (Cronjob) 
“This trigger runs the Jenkins job on a schedule, like every night or every 10 minutes, even if there are no code changes. It’s mainly used for regular builds, nightly builds, and health checks.”
Example use: nightly build at 1 AM.

2) Poll SCM

“In Poll SCM, Jenkins checks the Git repository at a fixed time interval. If Jenkins finds any new commit, then it triggers the build. If there’s no change, it won’t run.”
Key point: Jenkins is polling (pulling) Git again and again.

3) GitHub Webhook

“In webhook, GitHub directly notifies Jenkins whenever code is pushed or a pull request is created. So Jenkins starts the build immediately. It’s faster and more efficient than Poll SCM.”
Key point: GitHub pushes the event to Jenkins.

4) Trigger after another job

“This trigger starts a job automatically after another job completes. We use it to create a pipeline flow like: Build job → Test job → Deploy job.”
Key point: job chaining / job dependency.

✅ 7) Plugins (Jenkins):
==========≈==============

What are Jenkins plugins?

“Plugins are add-ons in Jenkins. Jenkins by default has limited features, but plugins help us integrate Jenkins with other tools like Git, Maven, Docker, Kubernetes, SonarQube, AWS, etc.”

Why plugins are used?

“We use plugins to extend Jenkins functionality. Without plugins, Jenkins cannot connect to external tools or perform advanced CI/CD tasks.”