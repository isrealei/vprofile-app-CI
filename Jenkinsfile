def COLOR_MAP = [
    'SUCCESS': 'good', 
    'FAILURE': 'danger',
]

pipeline{

     agent any

    
      
     environment {
         NEXUSPASS = credentials('nexuspass')



     }

     stages {

        stage('Set up parameter'){
            steps {
                script {
                    properties([
                        parameters({
                            string(
                                defaultvalue: '',
                                name: 'BUILD',
                            ),
                            string(
                                defaultvalue: '',
                                name: 'TIME',
                            )
                        })
                    ])
                }
            }
        }
       
        stage('Ansible Deploy to prod') {
            steps {
                ansiblePlaybook( [
                playbook: 'ansible/site.yml',
                inventory: 'ansible/prod.inventory',
                credentialsId: 'applogin',
                installation: 'ansible',
                disableHostKeyChecking: true, 
                extraVars: [
                  USER: "admin" ,
                  PASS: "${NEXUSPASS}" ,
                  nexusip: "172.31.18.143",
                  reponame: "vprofile-release",
                  groupid: "QA",
                  time: "${env.TIME}",
                  build: "${env.BUILD}",
                  artifactid: "vproapp",
                  vprofile_version: "vproapp-${env.BUILD}-${env.TIME}.war"
                ],
                colorized: true ])
                
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
