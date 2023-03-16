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
        stage("Static code analysis"){
            steps{
                withSonarQubeEnv(credentialsId: 'sonar') {
                sh 'mvn clean package sonar:sonar'
            }
          
        }
    }
  
}
}