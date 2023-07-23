


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
        stage('Deploy to AWS') {
            steps {
                withCredentials([[$class: 'AwsBucketCredentialsBinding', credentialsId: '', passwordVariable: '22EHuRRVo0q0utELHz1IhMw4SwsMrKwUAjQmnjoS', usernameVariable: 'AKIA2XC2HHDLK2GHGDWR']]) {
               // some block
              }
               
            }
        }

    }
}
