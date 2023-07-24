


pipeline {
    agent any
    tools {
           maven "maven:3.9.3"
        }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
                
            }
        }
        stage('code review') {
            steps {
                withSonarQubeEnv('sonar-sever-8.9.2'){
                     sh 'mvn clean package sonar:sonar'
                }
            }
        }
        stage ('s3 uplaod artifact') {
            steps {
                s3Upload consoleLogLevel: 'INFO', dontSetBuildResultOnFailure: false, dontWaitForConcurrentBuildCompletion: true, entries: [[bucket: 'jenkins-artifat', excludedFile: '', flatten: false, gzipFiles: false, keepForever: false, managedArtifacts: false, noUploadOnFailure: false, selectedRegion: 'us-iso-east-1', showDirectlyInBrowser: false, sourceFile: '/target/my-app.jar', storageClass: 'STANDARD', uploadFromSlave: false, useServerSideEncryption: false]], pluginFailureResultConstraint: 'SUCCESS', profileName: 'jenkins', userMetadata: []
            }
        }
    }
}
