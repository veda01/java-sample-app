pipeline{
    agent any
    stages {
        stage("Build") {
            steps {
                sh 'mvn clean install'
               
            }
        }
      stage('Sonarqube Analysis') {
            environment {
                scannerHome = tool 'SonarQubeScanner'
            }
            steps {
                withSonarQubeEnv('ALM Prod Sonar') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
        stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true }
            }
        }
    }
}