pipeline{
    agent{label 'Jenkins-Agent'}
    tools{
        jdk 'Java17'
        maven 'Maven3'
    }
    environment{
        APP_NAME = "Project_CICD"
        RELEASE = "1.0.0"
        DOCKER_USER = "rajith08"
        DOCKER_PASS = 'dockerhub'
        IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
        IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
    }
    stages{
        stage("Cleanup Workspace"){
            steps{
                cleanWs()
            }
        }
        stage("Checkout from SCM"){
            steps{
                git branch: 'master', credentialsId: 'GitHub', url: 'https://github.com/rajith08/Project'
            }
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
        stage("SonarQube Analysis"){
           steps{
               script{
                   withSonarQubeEnv(credentialsId: 'Jenkins-SonarQube-Token'){
                       sh "mvn sonar:sonar"
                   }
               }
           } 
        }
        stage("Quality Gate"){
            steps{
                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'Jenkins-SonarQube-Token'
                }
            }
        }
    }
}
