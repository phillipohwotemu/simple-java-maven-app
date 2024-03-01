pipeline {
    agent any

    tools {
        // Make sure 'M3' matches the Maven version configured in your Jenkins Global Tool Configuration
        maven 'mvn:3.5.2'
    }

    stages {
        stage('Initialize') {
            steps {
                echo 'Starting build process'
                // Optional: clean local Maven repository
                // sh 'rm -rf .m2/repository'
            }
        }

        stage('Build') {
            steps {
                echo 'Building project'
                // mvn clean package will compile your code and package it into a JAR or WAR, depending on your project
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing project'
                // Run tests; this can be a part of the build step or separate, depending on your preference
                sh 'mvn test'
            }
            post {
                always {
                    // Collect test results or other reports
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application'
                // Add your deployment steps here
                // For example, you might copy the built artifact to a web server
                // sh 'scp target/myapp-1.0-SNAPSHOT.jar user@server:/path/to/deploy'
            }
            when {
                branch 'main' // Adjust this condition to fit your deployment strategy
            }
        }
    }

    post {
        success {
            echo 'Build succeeded'
        }
        failure {
            echo 'Build failed'
        }
    }
}
