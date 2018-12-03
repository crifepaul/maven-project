pipeline{
    agent any
	parameters{
		string(name: 'tomcat-dev', defaultValue: '34.217.85.124', description: 'staging server')
		string(name: 'tomcat-prod', defaultValue: '35.161.63.141', description: 'staging prod')
	}
	triggers{
		pollscm('* * * * *')
	}
	stages{
		stage('Build'){
			steps{
				sh 'mvn clean package'
			}
			post{
				echo 'Now Archiving'
				archiveArtifacts artifacts: '**/target/*.war'
			}
		}
		stage('Deployments'){
			parallel{
				stage('Deploy to Stage'){
					steps{
						sh "scp -i /root/tomcat-demo.pem **/target/*.war ec2-user@34.217.85.124:/var/lib/tomcat7/webapps"
					}
				}
				stage('Deploy to Production'){
					steps{
						sh "scp -i /root/tomcat-demo.pem **/target/*.war ec2-user@35.161.63.141:/var/lib/tomcat7/webapps"
					}
				}
			}
		}
	}	
}
