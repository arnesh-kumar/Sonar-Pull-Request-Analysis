# Sonar-Pull-Request-Analysis
To Learn how to do the pull request analysis using SonarQube
Use case: To enable developers scan their source code (delta) using the SonarQube on every pull request submitted in GitHub. 
The integration happens between GitHub, SonarQube and Jenkins
Note: You should have an account created in GitHub.com, have access to Jenkins and SonarQube servers. Alternately, you have install Jenkins & SonarQube on your laptop/computer.

Below are the steps that needs to be followed:
1. Login to GitHub and create a repository (public or private)
2. Under the repo create a file called HelloWorld.java and commit to master branch. 
3. Jenkins Settings
    - Go to Jenkins home and click on Manage Jenkins --> Configure System
    - Home directory = 	/Users/arneshkumar/.jenkins
    - SonarQube servers; click on Add SonarQube --> Name = SonarQube_test_instance, Server URL = https://<sonarqube test instance               url>.ca.com , Server authentication token = (take this by login into SonarQube --> My Account --> Security --> Generate New Token = <enter token name> --> click on Generate
    - Jenkins URL = http://localhost:9090/ or http://machine-name:9090/
    - GitHub Servers: Name = <give a name>, API URL = https://github.com/api/v3, Credentials = Add  --> jenkins (username/password)--> Add
    - Artifactory: Server ID = Artifactory_dev_instance, URL = http://xxxxx/artifactory
    - GitHub Pull Request Builder: GitHub Auth = https://github.com/api/v3, Shared secret = xxx, Credentials = Add  --> jenkins                 (username/password)--> Add
    - 
