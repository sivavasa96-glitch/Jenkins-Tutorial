Jenkins Scripted Vs Declarative Pipeline:
=====================================

    Jenkins supports two types of pipeline syntax, Scripted Pipelines and Declarative Pipelines. Both serve the same purpose, 
but their approach and syntax are different.

1. Scripted Pipeline:
=====================

    The Scripted Pipeline is the original pipeline syntax in Jenkins, and it is based on the Groovy scripting language. 
It provides flexibility and control over the pipeline process. It requires a better understanding of Groovy scripting for the 
implementation of the complex code.
exam:
node {
    stage('Build Step') {
        // Build the application
        sh 'mvn clean install'
    }
    stage('Test Step') {
        // Run tests
        sh 'mvn test'
    }
    stage('Deploy Step') {
        // Deploy the application
        sh 'deploy.sh'
    }
}

2. Declarative Pipeline:
==========================

    A Declarative Pipeline is a structured and simplified way to define a Jenkins CI/CD pipeline using a predefined syntax.
It is written in a file called Jenkinsfile and stored in the source code repository.

Think of it as a rule-based pipeline that is easy to read, easy to manage, and safe to use.

exam:
    pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/example/repo.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                sh 'scp target/app.jar user@server:/opt/app/'
            }
        }
    }
}

Explanation of Each Section:
===========================

🔹 pipeline
Root block that defines a Declarative Pipeline
🔹 agent any
Tells Jenkins to run the pipeline on any available agent/node
🔹 stages
Groups all pipeline stages
🔹 stage('Checkout')
Pulls code from Git repository
🔹 stage('Build')
Compiles and packages the application (JAR/WAR)
🔹 stage('Test')
Runs automated test cases
🔹 stage('Deploy')
Deploys application to server/environment

Why do we use Declarative Pipeline?:
========================================

We use Declarative Pipeline because it:

1. Is easy to understand (even for beginners)
2. Has built-in syntax validation before execution
3. Follows best practices automatically
 4. Is less error-prone than Scripted Pipeline
5. Is recommended by Jenkins for most CI/CD projects
6. Works very well with Git, Maven, Docker, Kubernetes

👉 In real projects, teams prefer Declarative because multiple people can maintain it easily.

Note: Declarative Pipeline is structured, readable, and safe, while Scripted Pipeline is flexible but complex.

Note: Declarative Pipeline is a Jenkins pipeline style that uses a predefined syntax, making CI/CD pipelines easy to write, 
validate, and maintain.