pipeline {
  agent any
  stages {     
    stage("BuildCode") {
            steps {
                sh 'mvn clean install'
               
            }
    }
    stage('Unit-Test') {
            steps {
                sh 'mvn test'
            }
    }
    stage('Sonarqube Analysis') {
          environment {
              scannerHome = tool 'SonarQubeScanner'
          }
          steps {
              withSonarQubeEnv('sonarqube') {
                  sh '''${scannerHome}/bin/sonar-scanner \
                      -Dsonar.login=1c51a50be1cee3efc23de1b7c6705a40326f8900
                  '''
              }
          }
    }
    stage("Quality Gate") {
          steps {
              timeout(time: 3, unit: 'MINUTES') {
              waitForQualityGate abortPipeline: true, credentialsId: 'sonartoken'}
          }
    }
    stage ('Deploy To Prod') {
        input{
          message "Do you want to proceed for production deployment?"
        }
        steps {
                    sh 'echo "Deploy into Prod"'

          }
    }
  } 
post {
        always {
            emailext body: 'A Test EMail', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'
        }
}
  /// post {

  //     aborted {

  //       echo "Sending message to Slack"
  //       slackSend (color: "${env.SLACK_COLOR_WARNING}",
  //                 channel: "${params.SLACK_CHANNEL_2}",
  //                 message: "*ABORTED:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} by ${env.USER_ID}\n More info at: ${env.BUILD_URL}")
  //     } // aborted

  //     failure {

  //       echo "Sending message to Slack"
  //       slackSend (color: "${env.SLACK_COLOR_DANGER}",
  //                 channel: "${params.SLACK_CHANNEL_2}",
  //                 message: "*FAILED:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} by ${env.USER_ID}\n More info at: ${env.BUILD_URL}")
  //     } // failure

  //     success {
  //       echo "Sending message to Slack"
  //       slackSend (color: "${env.SLACK_COLOR_GOOD}",
  //                 channel: "${params.SLACK_CHANNEL_1}",
  //                 message: "*SUCCESS:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} by ${env.USER_ID}\n More info at: ${env.BUILD_URL}")
  //     } // success

  // } // post
        
        
}
