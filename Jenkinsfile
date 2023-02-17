
node{
    
    try{
    
    def mavenHome = tool name: "maven-3.8.7"
    
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])



//getting the code from git

stage('checkout code'){

sendslacknotification("STARTED")

git branch: 'development', url: 'https://github.com/BashettyRohith/maven-web-application.git'

}



//build
stage('build'){
    
    sh "${mavenHome}/bin/mvn clean package"

//bin-we use bin directory becz mvn is present in bin
}

//creating sonarqube report

/*

stage('sonarqube'){

   sh "${mavenHome}/bin/mvn sonar:sonar"

}

//upload articrafts in to nexus

stage('upload artifract'){

sh "${mavenHome}/bin/mvn deploy"
}

stage('upload tomcat'){


sshagent(['77d81bfd-3230-4199-a6d4-fd4da867fbe8']) {
   sh "scp -o  StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.233.160.169:/opt/apache-tomcat-9.0.70/webapps/"

}

}
*/
     
      
        
        
    }//tryclosing
    
       catch (e) {
    // If there was an exception thrown, the build failed
    currentBuild.result = "FAILURE"
    
  } finally {
    // Success or failure, always send notifications
    sendslacknotification(currentBuild.result)
  }
}//node closing


def sendslacknotification(String buildStatus = 'STARTED') {
  // build status of null means successful
  buildStatus =  buildStatus ?: 'SUCCESS'

  // Default values
  def colorName = 'RED'
  def colorCode = '#FF0000'
  def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
  def summary = "${subject} (${env.BUILD_URL})"

  // Override default values based on build status
  if (buildStatus == 'STARTED') {
    color = 'YELLOW'
    colorCode = '#FFFF00'
  } else if (buildStatus == 'SUCCESS') {
    color = 'GREEN'
    colorCode = '#00FF00'
  } else {
    color = 'RED'
    colorCode = '#FF0000'
  }

  // Send notifications
  slackSend (color: colorCode, message: summary)
}
 

