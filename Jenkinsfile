pipeline {
  agent {label 'slave1'}
  tools {
    maven 'M2_HOME'
  }
  stages{
    stage("Source code check out"){
    steps{
    echo "<---------------git fetch started--------------->"
    git 'https://github.com/prajwal8120/Vlai.git'
    echo "<---------------git fetch stopped--------------->"
      }
    }
  }
}
