node{
    
    stage('Clone repo'){
        git credentialsId: 'powhotemu', url: 'https://github.com/phillipohwotemu/simple-java-maven-app.git'
    }
    
    stage('Maven Build'){
        def mavenHome = tool name: "maven:3.9.3", type: "maven"
        def mavenCMD = "${mavenHome}/bin/mvn"
        sh "${mavenCMD} clean package"
    }
    
    stage('SonarQube analysis') {       
        withSonarQubeEnv('sonar-sever-8.9.2') {
       	sh "mvn sonar:sonar"    	
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
		version: '4.0.0'
	}
}
    
    stage('Build Image'){
        sh 'docker build -t ashokit/mavenwebapp .'
    }
    
    stage('Push Image'){
        withCredentials([string(credentialsId: 'DOCKER-CREDENTIALS', variable: 'DOCKER_CREDENTIALS')]) {
            sh 'docker login -u ashokit -p ${DOCKER_CREDENTIALS}'
        }
        sh 'docker push ashokit/mavenwebapp'
    }
    
    stage('Deploy App'){
        kubernetesDeploy(
            configs: 'maven-web-app-deploy.yml',
            kubeconfigId: 'Kube-Config'
        )
    }    
}
