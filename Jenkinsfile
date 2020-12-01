pipeline {
	agent {
		docker { image 'maven' }
	}
	stages {
		stage ('Checkout') {
			steps {
				git branch:'master', url: 'https://github.com/tanweihan/Vulnerable-Web-Application.git'
			}
		}
		
		stage ('Code Quality Check via SonarQube') {
			steps {
				script {
					def scannerHome = tool 'SonarQube';
					withSonarQubeEnv(){
					sh "${tool*("SonarQube")}/bin/sonar-scanner \
					  -Dsonar.projectKey=OWASP \
					  -Dsonar.sources=. \
					  -Dsonar.host.url=http://192.168.50.128:9000 \
					  -Dsonar.login=1e32199a9a27eb2ce6bc43793cbfdbb46052de0d"
					}
				}
			}
		}
	}
	post {
		always {
			recordIssues enabledForFailure: true, tool: sonarQube()
		}
	}
}
