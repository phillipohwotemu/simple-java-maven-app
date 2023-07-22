


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
        stage ('uplaod artifact') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'productcatalogue', classifier: '', file: 'target/productcatalogue', type: 'jar']], credentialsId: 'Nexus-credentials', groupId: 'kloud45', nexusUrl: '54.145.126.153:8081', nexusVersion: 'nexus2', protocol: 'http', repository: 'kloud45-snapshot-repository', version: '0.0.1-SNAPSHOT'
            }
        }
    }
}
