

pipeline {
    agent any
    tools {
           maven "maven:3.9.3"
        }
    environment {
        NEXUS_VERSION = "nexus2"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "http://44.211.151.25:8081/"
        NEXUS_REPOSITORY = "maven-nexus-repo"
        NEXUS_CREDENTIAL_ID = "nexus-user-credentials"
    }
    
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
                
            }
        }
        stage('code review') {
            steps {
                withSonarQubeEnv('sonar-sever-8.9.2') {
                    sh 'mvn clean package sonar:sonar'
                }
            }
        }
                stage ('uplaod artifact') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'my-app', classifier: '', file: 'pom.xml', type: 'jar']], credentialsId: 'Nexus-credentials', groupId: 'in.jenkins-user', nexusUrl: '35.171.24.101:8081', nexusVersion: 'nexus2', protocol: 'http', repository: 'maven-nexus-repo', version: 'pom.version'
        }
    }
}




