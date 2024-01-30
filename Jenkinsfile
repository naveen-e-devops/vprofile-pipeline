// jenkins declarative pipeline syntax for vprofile application

pipeline {
 agent any
    tools {
        maven "maven-3"
         jdk "java-8"
    }
    stages{
        stage("scm"){
          steps{
              // clone source code from git
              git 'https://github.com/naveen-e-devops/vprofile-pipeline.git'
          }  
        }
        
        stage("BUILD"){
            steps{
                // compine the source code
                
                sh 'mvn package'
            }
        }
        stage("ansible-playbook-run"){
            steps{
                
            }
        }
        
}
}
