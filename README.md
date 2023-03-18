#####

### Hybrid Continuous Delivery

This project is titled as Hybrid because Jenkins will be used as Continuous Integration tool together with AWS PaaS and SaaS services.

Tools Used 

•	Jenkins (For continuous Integration and Continuous Delivery): The Jenkins server will be running on an EC2 instance.
•	AWS Elastic Beanstalk - Runtime environment for deploying the built artifacts.
•	AWS S3 bucket:  The artifact built from Jenkins will be uploaded to the S3 bucket.
•	IAM user: A new user with programmatic access will be created with some given permission. The user will be given S3 bucket full access and elastic-beanstalk administrative access.
•	SonarQube (For code analysis)
•	Maven (To build the artifact)
•	Git (Version control) 
•	Nexus Sonar type Repository (for the artifact storage and download)
•	Slack – For Notification
•	AWS CLI – for authentication. Jenkins will use the cli together with access key and secret key to authenticate into AWS to create resources. 


- JDK 1.8 or later
- Maven 3 or later
- MySQL 5.6 or later

### Technologies

- Spring MVC
- Spring Security
- Spring Data JPA
- Maven
- JSP
- MySQL

### Database

Here,we used Mysql DB
MSQL DB Installation Steps for Linux ubuntu 14.04:

- $ sudo apt-get update
- $ sudo apt-get install mysql-server

Then look for the file :

- /src/main/resources/accountsdb
- accountsdb.sql file is a mysql dump file.we have to import this dump to mysql db server
- > mysql -u <user_name> -p accounts < accountsdb.sql
