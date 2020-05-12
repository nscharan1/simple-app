pipeline{
    agent any;
    stages{
        stage('checkout'){
            steps{
                echo 'checkout from git'
                git 'https://github.com/nscharan1/simple-app.git'
            }
        }


        stage('Build'){
            steps{
                echo 'Build stage'
                sh 'mvn -f ${WORKSPACE}/pom.xml compile package'
            }
        }
        
        
        stage('Sonarqube') {
            environment {
            scannerHome = tool 'SonarQubeScanner'
            }
            steps {
                withSonarQubeEnv('SonarQubeServer') {
                sh "${scannerHome}/bin/sonar-scanner"
                }
                timeout(time: 10, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: true
                }
            }
        }
        
        
        stage('Deploy'){
            steps{
                echo 'Deploy stage'         
            }
        }
    }
}
