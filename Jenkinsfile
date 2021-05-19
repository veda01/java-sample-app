pipeline {
  agent any
  stages {     
    stage("Build") {
            steps {
                sh 'mvn clean install'
               
            }
    }
    stage('Test') {
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
                      -Dsonar.login=b72f70ac766d440ea5bd8a3b71550730d2cbc32a
                  '''
              }
          }
    }
    stage("Quality Gate") {
          steps {
              timeout(time: 1, unit: 'MINUTES') {
              waitForQualityGate abortPipeline: true , credentialsId: 'sonartoken'}
          }
    }
    // stage("Quality Gate") {
    //   steps {
    //       timeout(time: 2, unit: 'MINUTES') { 
    //           script {
    //             def qg = waitForQualityGate()
    //             if (qg.status != 'OK') {
    //                 error "Pipeline aborted due to quality gate failure: ${qg.status}"
    //             }
    //           }
    //       }
    //   }
    // }
    // stage(“Quality Gate Status Check”) {
    //     timeout(time: 1, unit: ‘HOURS’)// Just in case something goes wrong, pipeline will be killed after a timeout
    //     // had previously tried using waitForQualityGate() and waitForQualityGate(webhookSecretId: ‘<webhook_secret_text>’ with same result
    //     def qg = waitForQualityGate(webhookSecretId: ‘<webhook_secret_text>’, credentialsId: ‘<sonar_project_secret_text>’) // Reuse taskId previously collected by withSonarQubeEnv
    //     if (qg.status != ‘OK’) {
    //     error “Pipeline aborted due to quality gate failure: ${qg.status}”
    // }
    // stage("Wait for quality gate") {
    //     steps {
    //         timeout(time: 1, unit: 'HOURS') {
    //             // "true" means the pipelines will be set to "UNSTABLE" if quality gate fails.
    //             waitForQualityGate(abortPipeline: true, credentialsId: 'compte-robot-my-project-token-sonarqube')
    //         }
    //     }
    // }  
  } 
        
  // post {

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
