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
		stage('Test'){
			steps{
				echo 'Test stage'
			}
		}
		stage('Artifact upload'){
			steps{
				echo 'Artifact Upload stage'
				sh 'nexusArtifactUploader artifacts: [[artifactId: 'simple-app', classifier: '', file: '/var/lib/jenkins/workspace/formac/target/simple-app-1.0..war', type: 'war']], credentialsId: 'nexus3', groupId: 'in.javahome', nexusUrl: '3.95.149.40:8081/nexus', nexusVersion: 'nexus2', protocol: 'https', repository: 'Releases', version: '1.0''
			}
		}
		stage('Deploy'){
			steps{
				echo 'Deploy stage'			
			}
		}
    }
} 
