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
    }
  
}