pipeline{
    agent any
    stages{
        stage("Git Checkout"){
            steps{
                git branch: 'main', url: 'https://github.com/Sudip1012/Counter-app-CICD-.git'
            }
          
        }
        stage("UNIT TEST"){
            steps{
                sh 'mvn test'
            }
          
        }
        stage("Integration"){
            steps{
                sh 'mvn verify -DskipUnitTests'
            }
          
        }
        stage("Maven Build"){
            steps{
                sh 'mvn clean install'
            }
          
        }
        stage("static Analysis"){
            steps{
                script{
                 withSonarQubeEnv(credentialsId: 'sonar') {
                sh 'mvn clean package sonar:sonar'
                  }   
                }
            }
        }
        stage("SonarQube Analysis"){
            steps{
                script{
                 withSonarQubeEnv(credentialsId: 'sonar') {
                sh 'mvn clean package sonar:sonar'
                  }   
                }
            }
        }
        stage("Quality Gate"){
            steps{
                script{
                 waitForQualityGate abortPipeline: false, credentialsId: 'sonar'  
                }
            }
        }
        stage("Uplode file to repo"){
            steps{
                script{
                    def readPomVersion = readMavenPom file: 'pom.xml'
                    
                    def nexusRepo = readPomVersion.version.endsWith('SNAPSHOT') ? "Demo-mvn-snap" : "Demo-Maven"
                 
                 nexusArtifactUploader artifacts: 
                 [
                    [
                        artifactId: 'springboot', 
                        classifier: '', 
                        file: 'target/Uber.jar', 
                        type: 'jar'
                        ]
                ],
                         credentialsId: 'nexus-auth', 
                         groupId: 'com.example', 
                         nexusUrl: '34.125.242.107:8081', 
                         nexusVersion: 'nexus3', 
                         protocol: 'http', 
                         repository: nexusRepo, 
                         version: "${readPomVersion.version}"
                }
            }
        }
  
}
}