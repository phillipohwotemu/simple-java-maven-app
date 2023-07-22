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
        
        stage('upload war to nexus'){
	       steps{
		        nexusArtifactUploader artifacts: [	
			     [
				      artifactId: 'my-app',
				      classifier: '',
				      file: 'target/my-app.jar',
				      type: jar		
			    ]	
		  ],
		credentialsId: 'nexus3',
		groupId: 'in.ashokit',
		nexusUrl: '',
		protocol: 'http',
		repository: 'maven-nexus-repo'
		version: '1.0-SNAPSHOT'
	}
}
    

        )
    }    
}
