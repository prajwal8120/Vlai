pipeline {
  agent {label 'slave1'}
  tools {
    maven 'M2_HOME'
  }
  stages{
    stage("Source code check out"){
    steps{
    echo "<--------------------git fetch started-------------------->"
    git 'https://github.com/prajwal8120/Vlai.git'
    echo "<--------------------git fetch stopped-------------------->"
      }
    }

    stage("Build Package"){
      steps{
        echo "<--------------------Building package started-------------------->"
        sh 'mvn clean compile'
        echo "<--------------------Building package started-------------------->"
      }
    }
  }
}
