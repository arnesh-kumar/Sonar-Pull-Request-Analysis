# Sonar-Pull-Request-Analysis
To Learn how to do the pull request analysis using SonarQube
Use case: To enable developers scan their source code (delta) using the SonarQube on every pull request submitted in GitHub. 
The integration happens between GitHub, SonarQube and Jenkins
Note: You should have an account created in GitHub.com, have access to Jenkins and SonarQube servers. Alternately, you have install Jenkins & SonarQube on your laptop/computer.

Below are the steps that needs to be followed:
1. Login to GitHub and create a repository (public or private)
2. Under the repo create a file called HelloWorld.java and commit to master branch. 
3. Jenkins Settings: Jenkins home --> Manage Jenkins --> Manage Plug-ins
    - Go to "Available" tab --> check the plug-ins to be installed & version --> click on "Install without restart"
    - Install the following plug-ins: Artifactory (if you want to use it), GitHub Integration Plugin (for jenkins), GitHub Pull Request         Builder, Green Balls, Pipeline (A suite of plugins that lets you orchestrate automation, simple or complex), Pipeline: GitHub Groovy        Libraries, SonarQube Scanner for Jenkins, SSH Slaves Plugin, Timestamper, Workspace Cleanup Plugin
4. Jenkins Settings: Jenkins home --> Manage Jenkins --> Global Tool Configuration
    - Git: Git installations --> Name = Default, Path to Git Executable = git
    - SonarQube Scanner: Add SonarQube Scanner --> SonarQube Scanner Name = <SonarQube_Jenkins> --> check Install automatically -->             Install from Maven Central --> select a latest version
5. Jenkins Settings: Jenkins home --> Manage Jenkins --> Configure System
    - Home directory = 	/Users/arneshkumar/.jenkins
    - SonarQube servers; click on Add SonarQube --> Name = SonarQube_test_instance, Server URL = https://<sonarqube test instance               url>.ca.com , Server authentication token = (take this by login into SonarQube --> My Account --> Security --> Generate New Token = <enter token name> --> click on Generate
    - Jenkins URL = http://localhost:9090/ or http://machine-name:9090/
    - GitHub Servers: Name = <give a name>, API URL = https://github.com/api/v3, Credentials = Add  --> jenkins (username/password)--> Add
    - Artifactory: Server ID = Artifactory_dev_instance, URL = http://xxxxx/artifactory
    - GitHub Pull Request Builder: GitHub Auth = https://github.com/api/v3, Shared secret = xxx, Credentials = Add  --> jenkins                 (username/password)--> Add
6. Jenkins --> New Item --> Enter an item name = HelloWorld --> click on Freestyle project --> OK
    - click on project name --> Configure
    - General: Description = Hello World
    - GitHub project: Project url = <go to GitHub -- Repo Name -- Clone or Download -- https://github.com/arnesh-kumar/Sonar-Pull-Request-          Analysis/)
    - Source Code Management: Git --> Repository URL = https://github.com/arnesh-kumar/Sonar-Pull-Request-Analysis.git --> Credentials -->          Add (enter user/pass to access GitHub)
    - Branches to build: Branch Specifier = ${sha1}
    - Build Triggers: check GitHub Pull Request Builder --> GitHub API credentials = https://github.com/api/v3 --> Admin list = <username>
        --> check "Use GitHub hooks for build triggering"
    - Build: Execute shell --> Command = 
            pwd 
            whoami
            cat ${WORKSPACE}/README.md
    - Add build step: Execute SonarQube Scanner: select the SonarQube Installation = SonarQube_test_instance, Task to run = scan, Path to           project properties = sonar-project.properties (see the sonar-project.properties file under this repo)
           Analysis properties = 
                sonar.github.pullRequest=${ghprbPullId}
                sonar.github.oauth= 4c879897f0ca82ce3f991b513dd1784a2698f43f 
            Additional arguments = -X
    - 
