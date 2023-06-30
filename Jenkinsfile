

pipeline {
    agent any
    tools {
            mymaven "maven:3.6.3"
        }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
                achive 'target/*.jar'
            }
        }
    }
}


