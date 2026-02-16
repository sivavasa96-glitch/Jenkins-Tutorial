🔥 CI/CD Pipeline Scenarios:
=============================

1) Explain your real-time Jenkins CI/CD pipeline flow from Git push to deployment.

“In my project, once developer pushes code to GitHub, GitHub webhook triggers Jenkins. Jenkins pulls the code, runs build and unit tests, then runs SonarQube quality scan. After that it creates artifact and builds Docker image, tags it with build number or git commit, and pushes to registry like DockerHub/ECR. Then Jenkins deploys to Dev/QA/UAT/Prod using Kubernetes or server. Finally it verifies deployment using pod status/health check and sends notification. If deployment fails, rollback happens.”

2) How do you design Jenkins pipeline for Java / NodeJS application?

“I design it stage wise: checkout → build → test → code quality → package → docker build → docker push → deploy → verify. For Java I use Maven stages, for Node I use npm ci and npm build. I keep Jenkinsfile in Git, use credentials store for secrets, and deploy only from main branch.”

3) How do you handle multiple environments in Jenkins (Dev, QA, UAT, Prod)?

“We handle multiple environments using parameters and separate deployment stages. Like Dev deploy happens automatically after build, QA and UAT may need manual approval, and Prod always needs approval. Each environment has separate namespace, config values, and credentials.”

4) How do you deploy the same build to multiple environments without rebuilding again?

“We build once and promote the same artifact. For example we build one Docker image, tag it with commit ID, push it to registry, and then deploy the same image tag to Dev → QA → UAT → Prod. So no rebuild, only promotion.”

5) How do you do rollback in Jenkins if deployment fails?

“Rollback depends on deployment type. In Kubernetes, we use kubectl rollout undo deployment. In servers, we keep previous artifact version and redeploy it. Jenkins pipeline will detect failure and trigger rollback automatically or with manual approval.”

🔥 Git + Branching Scenarios:
===============================

6) How do you build only when code changes happen in GitHub?

“We use GitHub webhook. Whenever a push happens, webhook triggers Jenkins instantly. This is better than Poll SCM because polling wastes resources.”

7) What is Multibranch Pipeline? How did you use it in your project?

“Multibranch pipeline automatically detects branches in Git and runs pipeline for each branch based on Jenkinsfile. In my project, feature branches run build and test, but only main branch triggers deployment.”

8) How do you run pipeline only for main branch and skip feature branches?

“In Jenkinsfile, we use when { branch 'main' } condition for deploy stages. So feature branches only build and test, but deployment happens only from main.”

9) How do you trigger Jenkins automatically when PR is raised?

“We integrate GitHub PR triggers using webhook and multibranch pipeline. When PR is created or updated, Jenkins runs build and tests automatically to validate the PR.”

10) How do you manage Jenkinsfile in Git?

“Jenkinsfile is stored inside the application repo. So pipeline code is version controlled, and any change is tracked. This is best practice because pipeline and application stay together.”

🔥 Jenkins Credentials + Security Scenarios:
===============================================

11) How do you store GitHub token / DockerHub password securely in Jenkins?

“We store secrets inside Jenkins Credentials Manager. Then in pipeline we use withCredentials. We never hardcode passwords inside Jenkinsfile.”

12) What is Jenkins secrets folder?

“Jenkins secrets folder is inside $JENKINS_HOME/secrets. It stores encryption keys and sensitive internal data used by Jenkins to encrypt credentials. It is very important in backup and restore.”

13) How do you restrict job access to specific teams?

“We use Role Based Authorization Strategy plugin. We create roles like dev, qa, admin and give permissions only to required jobs and folders.”

14) How do you manage role-based access control in Jenkins?

“Using RBAC plugin, we create global roles and project roles. Global roles control overall access, and project roles control job-level access.”

15) How do you prevent developers from seeing production credentials?

“We separate credentials per environment and restrict access using RBAC. Developers can access dev creds only, and prod creds are visible only to admins or release team.”

🔥 Agents / Nodes Scenarios:
================================

16) Why do we use Jenkins agents?

“Agents are used to run builds on separate machines. It reduces load on controller, supports parallel builds, and helps run builds on different OS like Linux and Windows.”

17) How do you run Jenkins builds on multiple OS like Linux + Windows?

“We configure Linux and Windows agents. In Jenkinsfile we specify agent labels like agent { label 'windows' } or agent { label 'linux' } depending on requirement.”

18) How do you setup a Jenkins agent using SSH?

“We create a new node in Jenkins, choose SSH method, provide host IP, username, and SSH key. Jenkins connects and installs agent automatically.”

19) How do you handle agent offline issue?

“First I check network and SSH connectivity. Then check disk space, Java version, and agent logs. Many times agent goes offline due to resource issues like CPU/memory.”

20) How do you run Docker builds on Jenkins agents?

“Docker must be installed on agent. Jenkins user should have docker permission. Then pipeline runs docker build and push commands on agent.”

🔥 Docker + Jenkins Scenarios:
==================================

21) How do you build Docker images in Jenkins pipeline?

“In pipeline, after build stage, we run docker build -t image:tag . using Dockerfile. Usually we tag using build number or commit ID.”

22) How do you push Docker images to DockerHub / AWS ECR using Jenkins?

“We store registry credentials in Jenkins credentials. Then we login inside pipeline and push. For ECR, we use AWS CLI login command and push image.”

23) How do you handle Docker permission denied error in Jenkins?

“This happens when Jenkins user is not in docker group. We fix it by adding Jenkins user to docker group and restarting Jenkins. Or run docker using root, but group method is best.”

24) How do you clean old Docker images automatically in Jenkins server?

“We use cleanup commands like docker system prune -af in a scheduled job, or we set retention policy. This avoids disk full issue.”

25) How do you tag Docker images in Jenkins?

“Best practice is tagging with git commit ID or build number. Example: myapp:${BUILD_NUMBER} or myapp:${GIT_COMMIT}. For release, we also tag as latest.”

🔥 Kubernetes + Jenkins Scenarios:
=====================================

26) How do you deploy application to Kubernetes using Jenkins?

“Jenkins connects to cluster using kubeconfig or service account token. Then it runs kubectl apply or Helm deploy. Usually deployment YAML is updated with new image tag.”

27) How do you update Kubernetes deployment using new image tag?

“We use kubectl set image deployment/app container=image:tag. Or with Helm we update values file with new tag and run helm upgrade.”

28) How do you use Helm in Jenkins pipeline?

“We install Helm on Jenkins agent. In pipeline we run helm upgrade --install with environment-specific values. Helm makes deployments easy and consistent.”

29) How do you check Kubernetes pod status from Jenkins pipeline?

“We run kubectl get pods and kubectl rollout status deployment. If rollout fails, pipeline fails.”

30) How do you rollback Kubernetes deployment from Jenkins?

“We use kubectl rollout undo deployment/app. In Helm, we use helm rollback release revision.”

🔥 Jenkins Build Triggers:
============================

31) Difference between Poll SCM and Webhook? Which is better?

“Poll SCM means Jenkins keeps checking Git periodically. Webhook means GitHub notifies Jenkins instantly. In real-time, webhook is better because it is faster and saves resources.”

32) How do you trigger pipeline every day at 10 PM?

“We use Build periodically with cron. Example: 0 22 * * * for 10 PM daily.”

33) How do you trigger job after another job?

“We use downstream job trigger. Like after build job success, it triggers deploy job. In pipeline, we can call another job using build job:.”

34) How do you trigger Jenkins when Docker image is pushed?

“We can use registry webhook, like DockerHub webhook or ECR event triggers via AWS. That webhook triggers Jenkins job.”

35) How do you trigger Jenkins only if Dockerfile changes?

“We use when { changeset 'Dockerfile' } in Jenkins pipeline. So job runs only if that file is modified.”

🔥 Jenkins Plugins Scenarios:
================================

36) Which plugins did you use and why?

“We use Git plugin for SCM, Pipeline plugin for Jenkinsfile, Docker plugin for docker steps, Kubernetes plugin for k8s agents, SonarQube plugin for quality scan, and Email/Slack plugin for notifications.”

37) How do you handle plugin compatibility issues after Jenkins upgrade?

“Before upgrade, we take backup. Then we upgrade Jenkins in staging first, check plugin compatibility, update plugins, and only then upgrade production.”

38) How do you migrate plugins from old Jenkins to new Jenkins?

“We copy plugins folder from old $JENKINS_HOME/plugins to new Jenkins, and restart. Or install same plugins manually using plugin manager.”

39) How do you backup Jenkins including plugins?

“We backup full $JENKINS_HOME. It includes jobs, plugins, config, users, secrets. That is enough to restore full Jenkins.”

40) How do you check plugin versions in Jenkins?

“Go to Manage Jenkins → Manage Plugins → Installed tab. There you can see plugin name and version.”

🔥 Troubleshooting Scenarios:
==================================

41) Jenkins job suddenly started failing. How will you debug?

“First I check console output. Then check recent changes like code change, plugin update, or agent issue. I verify credentials, workspace, and dependency issues. Most answers are in console logs.”

42) Build is stuck in queue. What could be the reason?

“Common reasons are no available agents, executor count is zero, label mismatch, or node is offline. Sometimes job is waiting for resources.”

43) Disk space full on Jenkins server. What will you do?

“I clean old workspaces, build history, and old docker images. Also enable build discard policy. Then increase disk if needed.”

44) Jenkins is slow. How will you improve performance?

“We move builds to agents, reduce load on controller, clean old builds, increase JVM memory, disable unused plugins, and optimize jobs.”

45) Pipeline fails only sometimes (intermittent). How do you debug?

“Intermittent issues usually come from network, flaky tests, resource limits, or dependency download issues. I check timestamps, retry logic, agent stability, and logs.”

🔥 Jenkins Production Issues Scenarios:
========================================

46) How do you upgrade Jenkins in production safely?

“First we take backup. Then we upgrade Jenkins in staging, validate jobs, and then upgrade production during maintenance window. After upgrade, we check plugin updates and job runs.”

47) How do you take Jenkins backup before upgrade?

“Stop Jenkins and take tar backup of $JENKINS_HOME. That includes jobs, plugins, credentials, and secrets.”

48) How do you migrate Jenkins from one server to another?

“We install same Jenkins version on new server, copy $JENKINS_HOME from old to new, install same Java version, and restart Jenkins. That restores jobs, plugins, users, and configs.”

49) How do you move Jenkins jobs from one Jenkins to another?

“We can copy job folders from $JENKINS_HOME/jobs to new Jenkins. Or export/import job config.xml. If we copy full home, all jobs move automatically.”

50) How do you restore Jenkins after crash?

“We install Jenkins again, then restore $JENKINS_HOME backup. Start Jenkins service, and verify jobs, plugins, credentials, and nodes.”