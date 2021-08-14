pipeline {
  agent any
  stages {     
    stage("BuildCode") {
            steps {
                sh 'mvn clean install'
                // stash includes: "./target/*.jar", name: "getJars"
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
                    mkdir dummy
                    // unstash 'getJars'
                    // sh 'ls -lrt'
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
