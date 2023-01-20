def registry  = 'https://bossu.jfrog.io'
def version   = '1.0.1'
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

    //stage("Sonar Code Analysis"){
      //environment {
        //       scannerHome = tool 'sonarscanner'
        //    }
     // steps{
     //   echo "<-------------------------Analysis started------------------------->"
     //   withSonarQubeEnv('sonarserver') {
     //               sh "${scannerHome}/bin/sonar-scanner"
//}
      //  echo "<-------------------------Analysis stopped------------------------->"
     // }
  //  }

    //stage ("Quality Gate") {

            //steps {
                //script {
        //echo "<-------------------------Quality Gate started------------------------->" 
                 //   timeout(time: 1, unit: 'HOURS') {
                 //       def qg = waitForQualityGate()
                 //       if(qg.status!='OK'){
                 //         error "Pipeline failed due to the Quality gate issue"   
                 //       }    
                //    }    
        //echo "<-------------------------Quality Gate stopped------------------------->"
        //        }    
        //    }   
     //   }
      
      stage("Jar Publish") {
            steps {
                script {
                        echo '<--------------- Jar Publish Started --------------->'
                         def server = Artifactory.newServer url:registry+"/artifactory" ,  credentialsId:"artifactorycredentialid"
                         def properties = "buildid=${env.BUILD_ID},commitid=${GIT_COMMIT}";
                         def uploadSpec = """{
                              "files": [
                                {
                                  "pattern": "jarstaging/(*)",
                                  "target": "maven-challenge/{1}",
                                  "flat": "false",
                                  "props" : "${properties}",
                                  "exclusions": [ "*.sha1", "*.md5"]
                                }
                             ]
                         }"""
                         def buildInfo = server.upload(uploadSpec)
                         buildInfo.env.collect()
                         server.publishBuildInfo(buildInfo)
                         echo '<--------------- Jar Publish Ended --------------->'  
                
                }
            }   
        }          
  }
}