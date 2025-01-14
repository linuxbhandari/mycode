pipeline {
    agent { label 'jenkins-agent-vm1' }
    tools {
      jdk 'Java21'
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
                git branch: main, credentialsId: 'github', url: 'https://github.com/linuxbhandari/mycode'
              } 
         }
         stage("Build Application"){
                steps {
                 sh "mvn clean package"
              }
         }
         stage{"Test Application"}
                steps {
                    sh "mvn test"
         }

       }
    }
}
