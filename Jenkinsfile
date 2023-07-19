

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
        stage('build & SonarQube analysis') {
            withSonarQubeEnv {sonar-sever-8.9.2}{
                sh 'mvn clean package sonar:sonar' 
            }
        }
    }
}


