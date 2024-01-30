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
              git branch: 'ansible-pipeline', url: 'https://github.com/naveen-e-devops/vprofile-pipeline.git'
          }  
        }
        
        stage("BUILD"){
            steps{
                // compine the source code
                
                sh 'mvn package'
            }
        }
        stage("list of files"){
            steps{
                // compine the source code
                
                sh 'ls -l'
            }
        }
        stage("ansible-playbook-run"){
            steps{
                ansiblePlaybook become: true, becomeUser: 'ansadm', credentialsId: 'ansible-ubuntu', disableHostKeyChecking: true, playbook: 'sample-playbook.yml', vaultTmpPath: ''
            }
        }
        
}
}
