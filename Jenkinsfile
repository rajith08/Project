pipeline{
agent { label 'Jenkins-Agent'}
tools{
    jdk 'Java17'
    maven 'Maven3'
  }
stages{
   stage("Cleanup Workspace"){
     steps{
	cleanWs()     
     }
   }
 stage("Checkout from SCM"){
   git branch: 'master', credentialsId: 'GitHub', url: 'https://github.com/rajith08/Project'
 }
stage("Build Application"){
	steps{
       sh "mvn clean package"
	}
     }
stage("Test Application"){
	steps{
       sh "mvn test"
	 }
      }
   }
}
