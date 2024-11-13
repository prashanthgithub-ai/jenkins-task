# jenkins-task
# Jenkins
1. Install Java using command ‘apt install openjdk-17-jre’.
2. Clone the jenkins file from the git repository go to that repo excute the file to install jenkins.
3. Use ‘systemctl start jenkins’ to start Jenkins.
4. Access Jenkins at http://localhost:8080.
# SonarQube
1. Install Java using command ‘apt install openjdk-17-jre’.
2. Add a user named sonaqube using command ‘adduser sonaqube’.
3 Switch to that use ‘su – sonarqube’ and make sure that zip is installed in the terminal are not
before switching the user.
4 wget before this link to download sonarqube to you terminal
5. Extract the downloaded zip file.
6. Navigate to the sonarqube directory bin there ‘sh sonar.sh start’ use that command to start the
sonarqube .
7. Access SonarQube at http://localhost:9000.
8. Configure database and authentication settings.
# Nexus
1. Install Java using command ‘apt install openjdk-17-jre’.
2. wget before this link to download nexus file in to your terminal
4. Extract the downloaded tar file using ‘tar -zxvf filename’
5. Add a user with a name nexus and make that user as the owner to the extracted files and give all
the permission to directories.
6. Make changes in the nexus.rc file and add nexus in the file.
7. Now start the nexus using systemctl start nexus.
8. Access Nexus at http://localhost:8081.
Tomcat
1. Install Java using command ‘apt install openjdk-17-jre.
2. Download Tomcat Extract the downloaded tar file
3. Navigate to the tomcat directory move to bin there run startup.sh.
4. Access Tomcat at http://localhost:8080.
    # note : Before integrating make sure to install the required plugin like sonarscanner, nexus artifactory, deploy as a container
 SonarQube-Jenkins pipeline syntax
1. Log in to Jenkins as an administrator.
2. Go to Manage Jenkins > Configure System.
3. Scroll down to SonarQube section.
4. Enter SonarQube URL, username, and password.
5. Click Save.
6. Create a new Jenkins job.
7. Add SonarQube Scanner build step.
8. Configure SonarQube settings.
9. Now go to the pipeline syntax and select with sonarscanner.
10. Provide the necessary details like username and password.
11. Click on generate pipeline syntax.
12. Select the pipeline syntax and copy it and paste to pipeline in pipeline job
    stage('sonarqube scanner') {
 steps {
 withSonarQubeEnv('sonarqube') {
 sh 'mvn sonar:sonar'
}
 }
 }
 if using pipeline job go to pipeline syntax select with sonarscanner and do the necessary step to
generate the pipline syntax.
Nexus-Jenkins pipeline syntax
1. Log in to Jenkins as an administrator.
2. Go to pipeline syntax and click on nexus artifacts.
3. Scroll down to nexus section.
4. Enter Nexus URL, username, and password.
5. Click on generate pipeline syntax.
6. Select the pipeline syntax and copy it and paste to pipeline in pipeline job
tage('nexus') {
 steps {
 nexusArtifactUploader artifacts: [[artifactId: 'vprofile', classifier: '', file: 'target/vprofilev2.war', type: 'war']], credentialsId: 'nexus', groupId: 'com.visualpathit', nexusUrl:
   '13.126.57.128:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'project', version: 'v2'
 }
}
Tomcat-Jenkins Integration
1. Log in to Jenkins as an administrator.
2. Go to pipeline syntax and select deploy war/ear to container.
3. Scroll down to Tomcat section.
4. Enter Tomcat URL, username, and password.
5. Add necessary details and generate pipeline syntax.
6. Select the pipeline syntax and copy it and paste to pipeline in pipeline job
stage('tomcat deploy') {
 steps {
 deploy adapters: [tomcat9(credentialsId: 'tom', path: '', url: 'http://15.0.22.34:8080/')],
contextPath: 'vprofile', war: 'target/*.war'
 }
 # pipeline sytanx
 pipeline {
    agent any
 
    stages {
        stage('git checkout') {
            steps {
               git branch: 'main', url: 'https://github.com/prashanthgithub-ai/task.git' 
            }
        }
        stage('git build') {
            steps {
               sh 'mvn clean package' 
            }
        }
        stage('sonar scaner') {
            steps {
               withSonarQubeEnv('sonarqube') {
    sh 'mvn sonar:sonar'
} 
            }
        }
        stage('nexus uploader') {
            steps {
               nexusArtifactUploader artifacts: [[artifactId: 'myweb', classifier: '', file: 'target/myweb-8.6.2.war', type: 'war']], credentialsId: 'nexus', groupId: 'in.javahome', nexusUrl: '13.126.57.128:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'pipeline', version: '8.6.2' 
            }
        }
        stage('deploy') {
            steps {
               deploy adapters: [tomcat9(credentialsId: 'deploy', path: '', url: 'http://15.0.22.34:8080/')], contextPath: 'zomato', war: 'target/*.war'
            }
        }
    }
}
![Screenshot (69)](https://github.com/user-attachments/assets/5ceaad60-2b98-4311-93dd-7c60c7ae7aac)
Nexus Artifact
![Screenshot (69)](https://github.com/user-attachments/assets/4f401aba-b575-437e-b02f-8cef0c2a6e2b)
![Screenshot (68)](https://github.com/user-attachments/assets/2f01b81c-658b-4d0b-8e3f-31acc0538202)


 
