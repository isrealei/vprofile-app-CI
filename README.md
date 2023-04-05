#####

### Hybrid Continuous Delivery

This project is titled as Hybrid because Jenkins will be used as Continuous Integration tool together with AWS PaaS and SaaS services. •	Hybrid Continuous Delivery

This project is a ci/cd hybrid project where Jenkins fetch the applications code, builds it using Maven, tests it, scans the code using sonar scanner and upload the result to SonarQube server for code analysis and quality gates, and finally uploads the artifacts to nexus and AWS S3. The stored artifacts stored on the AWS s3 will then get deployed to elastic Beanstalk by updating the beanstalk environment with the new built artifact.

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

- Firstly, the project uses Jenkins as the CI/CD tool. Jenkins is responsible for fetching the code from the source code repository, which could be Git, SVN or any other source control management tool.

- Once the code is fetched, Jenkins uses Maven to build the application. Maven is a build tool that helps to manage dependencies and automate the build process.

- After the build is complete, Jenkins runs tests on the application. This is to ensure that the code is working as expected and to catch any errors that may have occurred during the build process.

- Next, Jenkins scans the code using a tool called Sonar Scanner. Sonar Scanner is a code analysis tool that identifies code quality issues and technical debt. The results of the code analysis are uploaded to a SonarQube server for further analysis and to enforce quality gates.

- After the code analysis is complete, Jenkins uploads the artifacts to both Nexus and AWS S3. Nexus is a repository manager that stores binary artifacts such as jars and wars. AWS S3 is an object storage service that stores files and objects.

- Finally, the artifacts stored on AWS S3 are deployed to Elastic Beanstalk by updating the Beanstalk environment with the newly built artifact. Elastic Beanstalk is a fully managed service that makes it easy to deploy and scale web applications and services.

### Summary

In summary, this CI/CD hybrid project uses Jenkins as the CI/CD tool, Maven for building the application, SonarScanner for code analysis, and Nexus and AWS S3 for artifact storage. The code analysis results are uploaded to SonarQube for further analysis, and the final artifacts are deployed to Elastic Beanstalk for production use.
