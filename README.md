#####

### Hybrid Continuous Delivery

This project is titled as Hybrid because Jenkins will be used as Continuous Integration tool together with AWS PaaS and SaaS services.


## Overview 

The new CI/CD pipeline includes the following steps:

- Jenkins is used to build and test the app on a remote server.
- If the tests pass, Ansible is used to deploy the app to a production server.
- Ansible also handles configuration management, ensuring that the production server is properly configured for the app.


### Tools Used 

-	Jenkins (For continuous Integration and Continuous Delivery): The Jenkins server will be running on an EC2 instance.
-	AWS Elastic Beanstalk - Runtime environment for deploying the built artifacts.
-	AWS S3 bucket:  The artifact built from Jenkins will be uploaded to the S3 bucket.
-	IAM user: A new user with programmatic access will be created with some given permission. The user will be given S3 bucket full access and elastic-beanstalk administrative access.
-	SonarQube (For code analysis)
-	Maven (To build the artifact)
- Ansible - an open-source automation tool used for configuration management and deployment.
- Docker - a containerization platform for creating and running applications.
-	Git (Version control) 
-	Nexus Sonar type Repository (for the artifact storage and download)
-	Slack – For Notification
-	AWS CLI – for authentication. Jenkins will use the cli together with access key and secret key to authenticate into AWS to create resources. 

### Configuration Files
The following files are included in this branch:

- Jenkinsfile - a script that defines the CI/CD pipeline using Jenkins and Ansible.
- Dockerfile - a file that defines the app's containerization settings.
- ansible/ - a directory containing Ansible playbooks and configuration files.



### Flow of Execution 

- This project is a continuation of a previous project. The pipeline used previously will be validated to ensure that it is still working correctly. 
- 	GitHub webhook will be updated with Jenkins IP to trigger build.
-	AWS CLI will be installed in the Jenkins server.
-	AWS Services
  - Create S3 bucket.
  - Create IAM user with access keys and beanstalk policy and s3 policy.
  - Create a Beanstalk environment.
-	Create a Jenkins file for both stages


### How to Use

To use this updated CI/CD pipeline for your own VProfile App:

- Clone this repository: git clone https://github.com/isrealei/vprofile-app-CI.git
- Check out the cicd-jenkins-ansible branch: git checkout cicd-jenkins-ansible
- Modify the Jenkinsfile and Ansible playbooks to include the appropriate build, test, and deployment steps for your app.
- Set up a Jenkins server to run the CI/CD pipeline.
- Connect the Jenkins server to your GitHub repository, and configure it to run the Jenkinsfile on every commit to the master branch.

