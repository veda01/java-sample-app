pipeline {
  agent any
  stages {     
    stage("BuildCode") {
            steps {
                sh 'mvn clean install'
                sh 'ls -lrt ./target/*'
            }
    }
    stage('Unit-Test') {
            steps {
                sh 'mvn test'
            }
    }

       
    stage ('Deploy To DEV') {
        steps {
                    sh 'echo "Deploy into Prod"'

          }
    }
       
    stage ('Deploy To UAT') {
        steps {
                    sh 'echo "Deploy into Prod"'

          }
    }    
    stage ('Deploy To Prod') {
        steps {
                    sh 'echo "Deploy into Prod"'

          }
    }
  } 
               
}
