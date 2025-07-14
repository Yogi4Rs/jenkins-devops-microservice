//declarative

pipeline {

	// agent any

	agent {docker {image 'maven:3.6.3'}}
	stages {
		stage('Build') {
			steps{
				sh 'maven --version'
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
	} 
	post {
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
