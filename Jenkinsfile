


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
            stage('Upload Artifacts to S3') {
      steps {
        awsS3Upload(pathStyleAccessEnabled: true, credentialsId: 'your-aws-credentials', bucket: 'your-s3-bucket', sourceFile: 'path/to/artifact.zip', targetPath: 'desired/s3/location/')
      }
    }
  }
}

