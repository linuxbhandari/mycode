pipeline {
    agent { label 'ubuntu-vm1-jenkins-agent' }
    tools {
      maven 'Maven3'
}
     stages {
         stage("Cleanup Workspace"){
                steps {
                cleanWs()
                }
         }
         stage("Checkout from SCM"){
                steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/linuxbhandari/mycode'
              } 
         }
         stage("Build Application"){
                steps {
                 sh "mvn clean package"
              }
         }
         stage("Test Application"){
                steps {
                    sh "mvn test"
         }

      }
         stage("SonarQube Analysis"){
	        steps {
		script {
		withSonarQubeEnv(credentialsId: 'jenkins-sonarqube-token') {
			     sh "mvn sonar:sonar"
        		}
	 	   }
	      }
  	 } 
 	 stage("Quality Gate"){
	      steps {
		script {
                     waitForQualityGate abortPipeline: false, credentialsId: 'jenkins-sonarqube-token'
	      }
	  }
      }  
   }
}
