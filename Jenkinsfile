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
               scannerHome = tool 'sonar-scanner'
            }
      steps{
        echo "<-------------------------Analysis started------------------------->"
        withSonarQubeEnv('sonar-server') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
        echo "<-------------------------Analysis stopped------------------------->"
      }
    }
  }
}
