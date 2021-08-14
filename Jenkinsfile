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

    stage ('Deploy To Prod') {
        input{
          message "Do you want to proceed for production deployment?"
        }
        steps {
                    sh 'echo "Deploy into Prod"'

          }
    }
  } 
               
}
