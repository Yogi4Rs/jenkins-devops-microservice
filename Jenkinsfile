//declarative

pipeline {

	agent any
	stages {
		stage('Build') {
			steps{
				echo "Build"
			}
		}
		stage('Test') {
			steps{
				echo "Test"
			}
		}
		stage('Integration Test'){
			steps{
				echo "Integration Test"
			}
		}
	} post {
		always {
			echo "I'm awesome and i run always"
			}
		success {
			echo "I run only when successful"
			}
		failure {
			echo "I run only when fail"
			}	
	}
}
