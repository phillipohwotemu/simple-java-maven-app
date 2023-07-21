

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
                withSonarQubeEnv('sonar-sever-8.9.2') {
                    sh 'mvn clean package sonar:sonar'
                }
            }
        }
        stage('artifact upload') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'my-app', classifier: '', file: 'pom.xml', type: 'jar']], credentialsId: 'nexus-user-credentials', groupId: 'com.mycompany.app', nexusUrl: '44.211.151.25:8081', nexusVersion: 'nexus2', protocol: 'http', repository: 'maven-nexus-repo', version: '1.0-SNAPSHOT'
            }
        }

    }
}


