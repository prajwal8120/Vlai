pipeline {
  agent {label 'slave1'}
  tools {
    maven 'M2_HOME'
  }
  stages{
    stage("Source code check out"){
    steps{
      sh 'printenv'
      echo "<-------------------------git fetch started------------------------->"
      git 'https://github.com/prajwal8120/Vlai.git'
      echo "<-------------------------git fetch stopped------------------------->"
      }
    }

    stage("Compile source code"){
      steps{
        echo "<------------------------Compile started------------------------->"
        sh 'mvn clean compile'
        echo "<------------------------Compile stopped------------------------->"
      }
    }

    stage("Build Package"){
      steps{
        echo "<-------------------------Building package started------------------------->"
        sh 'mvn clean package'
        echo "<-------------------------Building package stopped------------------------->"
      }
    }

    stage("Sonar Code Analysis"){
      environment {
               scannerHome = tool 'sonarscanner'
            }
      steps{
        echo "<-------------------------Analysis started------------------------->"
        withSonarQubeEnv('sonarserver') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
        echo "<-------------------------Analysis stopped------------------------->"
      }
    }

    stage ("Quality Gate") {

            steps {
                script {
        echo "<-------------------------Quality Gate started------------------------->" 
                    timeout(time: 1, unit: 'HOURS') {
                        def qg = waitForQualityGate()
                        if(qg.status!='OK'){
                          error "Pipeline failed due to the Quality gate issue"   
                        }    
                    }    
        echo "<-------------------------Quality Gate stopped------------------------->"
                }    
            }   
        }          
  }
}