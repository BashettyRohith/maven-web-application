
node{
    
    def mavenHome = tool name: "maven-3.8.7"
    
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])



//getting the code from git

stage('checkout code'){



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

}//node closing

