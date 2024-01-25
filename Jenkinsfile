pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven-3"
        jdk "java-8"
    }
    stages {
        stage('clone') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/naveen-e-devops/vprofile-pipeline.git'
            }
        }
        stage('Build'){
            //build vprofile project 
            steps {
                sh 'mvn package '
            }
        }
    }
}
