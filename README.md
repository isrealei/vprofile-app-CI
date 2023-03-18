#####

### Hybrid Continuous Delivery

This project is titled as Hybrid because Jenkins will be used as Continuous Integration tool together with AWS PaaS and SaaS services.

### Tools Used 

-	Jenkins (For continuous Integration and Continuous Delivery): The Jenkins server will be running on an EC2 instance.
-	AWS Elastic Beanstalk - Runtime environment for deploying the built artifacts.
-	AWS S3 bucket:  The artifact built from Jenkins will be uploaded to the S3 bucket.
-	IAM user: A new user with programmatic access will be created with some given permission. The user will be given S3 bucket full access and elastic-beanstalk administrative access.
-	SonarQube (For code analysis)
-	Maven (To build the artifact)
-	Git (Version control) 
-	Nexus Sonar type Repository (for the artifact storage and download)
-	Slack – For Notification
-	AWS CLI – for authentication. Jenkins will use the cli together with access key and secret key to authenticate into AWS to create resources. 


### Flow of Execution 

- This project is a continuation of a previous project. The pipeline used previously will be validated to ensure that it is still working correctly. 
- 	GitHub webhook will be updated with Jenkins IP to trigger build.
-	AWS CLI will be installed in the Jenkins server.
-	AWS Services
  - Create S3 bucket.
  - Create IAM user with access keys and beanstalk policy and s3 policy.
  - Create a Beanstalk environment.
-	Create a Jenkins file for both 




