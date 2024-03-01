pipeline {
    agent any

    tools {
        maven 'mvn:3.5.2' // Ensure 'M3' matches the Maven version configured in your Jenkins Global Tool Configuration
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building project...'
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
            post {
                always {
                    echo 'Test stage completed.'
                }
            }
        }
    }

    post {
        success {
            echo 'Build and Test Stages completed successfully.'
        }
        failure {
            echo 'An error occurred during the build/test process.'
        }
    }
}
