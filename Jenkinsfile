// This below function is to get the last build number of a auccessfull build from the staging pipeline
import jenkins.model.*
def buildNumber = jenkins.instance.getItem("cicd-jenkins-beanstalk-stage").lastSuccessfulBuild.number

def COLOR_MAP = [
    'SUCCESS': 'good', 
    'FAILURE': 'danger',
]

pipeline{

     agent any

     tools{
        maven "MAVEN3"
        jdk "OracleJDK8"
     }
      
     environment {
        SNAP_REPO = 'vprofile-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = "admin"
        RELEASE_REPO = 'vprofile-release'
        CENTRAL_REPO = 'vpro-maven-central'
        NEXUSIP = '172.31.18.143'
        NEXUSPORT = '8081'
        NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUS_LOGIN = 'nexuslogin'
        SONARSERVER = "sonarserver"
        SONARSCANNER = "sonarscanner"
        ARTIFACT_NAME = "vprofile-v${buildNumber}.war"
        AWS_S3_BUCKET = "isreal-kops-state"
        AWS_EB_APP_NAME = "delightapp"
        AWS_EB_ENVIRONMENT = "Delightapp-prod-env"
        AWS_EB_APP_VERSION = "${buildNumber}"
     }

     stages {

        stage("Deploy to AWS elastick beanstalk") {
            // Install pipeline: AWS steps and AWS SDK plugins on jenkins to run the withAWS method
            steps{
                withAWS(credentials: "awscreds", region: "us-east-1"){
                 
                // This command deploy the new application version to the beanstalk environment 
                sh "aws elasticbeanstalk update-environment --application-name $AWS_EB_APP_NAME --environment-name $AWS_EB_ENVIRONMENT --version-label $AWS_EB_APP_VERSION"
                
                  }
            }
            
        }
     }
     post {
        always {
            echo 'Slack Notifications.'
            slackSend channel: '#isreal-channel',
                color: COLOR_MAP[currentBuild.currentResult],
                message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} \n More info at: ${env.BUILD_URL}"
        }
    }

}
