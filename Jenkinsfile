


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
        stage('AWS Activate') {
            steps {
                // Install and configure AWS Activate plugin
                script {
                     // Install AWS Activate plugin
                    pluginInstallation('aws-activate@1.0.0')

                    // Configure AWS Activate plugin
                    configureAWSActivate()
                }
            }
        }

    }
}

def pluginInstallation(String plugin) {
    try {
        // Check if the plugin is already installed
        if (!jenkins.model.Jenkins.instance.pluginManager.plugins.find { it.shortName == plugin }) {
            // Install the plugin
            jenkins.model.Jenkins.instance.updateCenter.install(jenkins.model.Jenkins.instance.updateCenter.getPlugin(plugin))
        }
    }catch (Exception e) {
        // Handle any exceptions during plugin installation
        echo "Failed to install plugin: ${plugin}"
        error(e.toString())
    }
}
def configureAWSActivate() {
    try {
        // Configure AWS Activate plugin
        // Replace the placeholders with your AWS Activate credentials
        withAWSActivate(credentialsId: 'aws-activate-credentials', awsRegion: 'us-west-2') {
            // Your AWS Activate steps here
        }
    } catch (Exception e) {
        // Handle any exceptions during AWS Activate configuration
        echo "Failed to configure AWS Activate plugin"
        error(e.toString())
    }
}
