pipeline{
	agent any
	tools{
		maven 'localMAVEN'
		}
	stages{
		stage('Build'){
			steps{
				sh 'mvn clean package'
			}
		post{
			success{
				archiveArtifacts artifacts: '**/target/*.war'
			}
		}
		stage('Deploy to stage'){
			steps{
				build job: 'deploy-to-staging'
			}
		}		
	}
	}
}
