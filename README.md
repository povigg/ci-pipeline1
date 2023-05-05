# ci-pipeline1
CI pipeline using Jenkins, SonarQube and Nexus

## CI WorkFlow:

Developer will push code changes to GitHub. Jenkings will detect code changes and Fetch the code. Then Maven will be used to build the code and generate artifacts. Then we will use Maven tu run Unit Test, this will check if code works or not. After SunarQube will be run to find code vulnerabilities. The last, generated and checked artifact will be stored in Nexus


## Configure VMs

Start VMs using vagrant file

## Jenkins

Install Nexus Artifact Uploader, SonarQube Scanner, Build Timestamp, Pipeline Maven Integration and Pipeline Utility Steps plugins in Jenkins

Install JDK and Maven

JDK: Name - OracleJDK8
JAVA_HOME - /usr/lib/jvm/java-8-openjdk-amd64

Maven: NAME - MAVEN3

SonarQube: Name - sonar4.8
Integrate SonarQube server in Jenkins 'Configure System'. Check 'env. variables', add SonarQ server

## Write Jenkins Pipeline

