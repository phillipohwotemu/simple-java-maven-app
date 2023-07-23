


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
                scripts {
                      sh 'aws s3 cp my-artifact.zip s3://jenkins-artifat/my-artifact.zip'  // Example command to upload artifact to S3 bucket
                      sh 'aws cloudformation deploy --template-file my-template.yml --stack-name my-stack'  // Example command to deploy a CloudFormation stack
                         // Add more AWS CLI commands or SDK calls as needed

                }
            }
        }

    }
}
