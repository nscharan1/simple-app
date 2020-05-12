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



        stage('Artifact upload'){
            steps{
                echo 'Artifact Upload stage'
                nexusArtifactUploader artifacts: [[artifactId: 'simple-app', classifier: '', file: '/var/lib/jenkins/workspace/formac3/target/simple-app-1.0..war', type: 'war']], credentialsId: 'nexus2', groupId: 'in.javahome', nexusUrl: 'ec2-54-227-138-60.compute-1.amazonaws.com:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'releases', version: '1.0'
            }
        }
        
         stage('SonarQube Analysis') { 
            steps {
                echo 'Running SonarQube Analysis...'
            script {
                 def scannerHome = tool 'SonarQubeScanner'
                 withSonarQubeEnv('SonarQubeServer') {
                 sh """ ${scannerHome}/bin/sonar-runner -D sonar.login=admin -D sonar.password=admin """
                 }
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
