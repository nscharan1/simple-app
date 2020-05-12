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
        
        
        stage('Artifact upload'){
            steps{
                echo 'Artifact Upload stage'
                nexusArtifactUploader artifacts: [[artifactId: 'simple-app', classifier: '', file: '/var/lib/jenkins/workspace/formac3/target/simple-app-1.0..war', type: 'war']], credentialsId: 'nexus2', groupId: 'in.javahome', nexusUrl: '54.175.217.81:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'releases', version: '2.0'
            }
        }
        
        
        stage('Deploy'){
            steps{
                echo 'Deploy stage'         
            }
        }
    }
}
