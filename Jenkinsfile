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
        
  

}
}
