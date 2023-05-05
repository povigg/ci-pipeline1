# ci-pipeline1
CI pipeline using Jenkins, SonarQube and Nexus

## CI WorkFlow:

Developer will push code changes to GitHub. Jenkings will detect code changes and Fetch the code. Then Maven will be used to build the code and generate artifacts. Then we will use Maven tu run Unit Test, this will check if code works or not. After SunarQube will be run to find code vulnerabilities. The last, generated and checked artifact will be stored in Nexus


## Configure VMs

Start VMs using vagrant file

## Jenkins Plugins

Install Nexus Artifact Uploader, SonarQube Scanner, Build Timestamp, Pipeline Maven Integration and Pipeline Utility Steps plugins in Jenkins

