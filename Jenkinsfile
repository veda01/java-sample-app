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
                withSonarQubeEnv('sonarqube') {
                    sh "${scannerHome}/bin/sonar-scanner -Dsonar.login=560ed56a592f6302844117ce8f56b4dd7c217beb"
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