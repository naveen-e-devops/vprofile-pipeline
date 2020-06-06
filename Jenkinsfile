// jenkins declarative pipeline syntax for vprofile application

pipeline {
 agent any
    tools {
        maven "maven"
    }
    stages{
        stage("scm"){
          steps{
              // clone source code from git
              git 'https://github.com/naveen-e-devops/VProfile.git'
          }  
        }
        
        stage("BUILD"){
            steps{
                // compine the source code
                
                sh label: '', script: 'mvn package'
            }
        }
        
stage('sonarqube') {
         environment 
              {
              def scannerHome = tool 'sonarqube'
              }
       steps {
        withSonarQubeEnv('sonarqube') {
              sh "${scannerHome}/bin/sonar-scanner"
             }
       //timeout(time: 10, unit: 'MINUTES') {
       //waitForQualityGate abortPipeline: true
	  
      //}
       }
       }
       
       stage("nexus uploader"){
           steps{
               //uploading artifact into nexus repo
               nexusArtifactUploader artifacts: [[artifactId: 'vprofile', classifier: '', file: 'target/vprofile-v1.war', type: 'war']], credentialsId: '34952091-6fcc-4fc5-b1f5-df8a88f9daff', groupId: 'DEV', nexusUrl: '10.128.0.4:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'vprofile-repo', version: '$BUILD_ID'
               
           }
           
       }  

}
}
