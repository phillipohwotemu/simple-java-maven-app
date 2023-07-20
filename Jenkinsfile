

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
                nexusArtifactUploader artifacts: [[artifactId: 'my-app', classifier: '', file: 'target/my-app.jar', type: 'jar']], credentialsId: 'Nexus-credentials', groupId: 'kloud', nexusUrl: '54.145.126.153:8081/', nexusVersion: 'nexus2', protocol: 'http', repository: 'simple-java-maven-app', version: '1.0-SNAPSHOT'
            }
        }

    }
}


