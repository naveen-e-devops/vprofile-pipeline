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
       stage('CODE ANALYSIS with SONARQUBE') {
          
		  environment {
             scannerHome = tool 'sonarqube-4'
          }

          steps {
            withSonarQubeEnv('sonarqube') {
               sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=vprofile \
                   -Dsonar.projectName=vprofile-repo \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=src/ \
                   -Dsonar.login=admin \
                   -Dsonar.password=admin123 \
                   -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                   -Dsonar.junit.reportsPath=target/surefire-reports/ \
                   -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                   -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
            }

            //timeout(time: 1, unit: 'MINUTES') {
            //   waitForQualityGate abortPipeline: false
           // }
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
        stage('deploy to tomcat'){
            steps{
                deploy adapters: [tomcat8(credentialsId: 'tomcat-creds', path: '', url: 'http://172.31.4.186:8080')], contextPath: 'march-15', war: 'target/vprofile-v1.war'
            }
        }
    }
}
