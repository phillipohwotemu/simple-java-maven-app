


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
        stage('uplaod to s3') {
            try {
                withCredentials([<object of type com.cloudbees.jenkins.plugins.awscredentials.AmazonWebServicesCredentialsBinding>]) {
                sh "aws s3 ls"
                    sh "aws s3 cp addressbook_main/target/my-app.jar s3://cloudyeticicd2023-july-23/"
              }
            }  catch(err) {
                sh "echo error in sending artifacts to s3"
            }
        }

    }
}
