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
		stage('Quality Analysis'){
			steps{
					echo 'SonarQube Check'
    					def scannerHome = tool 'sonar7';
   					withSonarQubeEnv('Sonarqube') { // If you have configured more than one global server connection, you can specify its name
     					sh "${scannerHome}/bin/sonar-scanner"
  					}
  			}
		}
		stage('Artifact upload'){
			steps{
				echo 'Artifact Upload stage'
				nexusArtifactUploader artifacts: [[artifactId: 'simple-app', classifier: '', file: '/var/lib/jenkins/workspace/formac3/target/simple-app-1.0..war', type: 'war']], credentialsId: 'nexus', groupId: 'in.javahome', nexusUrl: 'ec2-52-90-176-242.compute-1.amazonaws.com:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'releases', version: '1.0'
			}
		}
		stage('Deploy'){
			steps{
				echo 'Deploy stage'			
			}
		}
	}
}
