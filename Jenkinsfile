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
        stage('Artifact uploader'){
            steps {
                nexusArtifactUploader(
                nexusVersion: 'nexus3',
                protocol: 'http',
                nexusUrl: '172.31.32.85:8081',
                groupId: 'DEV',
                version: '${BUILD_ID}',
                repository: 'vprofile-repo',
                credentialsId: 'nexus-creds',
                artifacts: [
                    [artifactId: 'vprofile-id',
                    classifier: '',
                    file: 'target/vprofile-v1.war',
                    type: 'war']
                    ]
                )
            }
        }
    }
}
