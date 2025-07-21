//declarative

pipeline {

	agent {
		docker {
			image 'maven:3.9.6-eclipse-temurin-17'
			args '-v /var/run/docker.sock:/var/run/docker.sock'
		}
	}


	// agent {docker {image 'maven:3.6.3'}}
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('Checkout') {
			steps{
				sh 'mvn --version'
				sh 'docker version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD ID - $env.BUILD_ID"
				echo "JOB NAME - $env.JOB_NAME"
				echo "BUILD TAG - $env.BUILD_TAG"
				echo "BUILD URL - $env.BUILD_URL"
			}
		}
		stage('Compile'){
			steps{
				sh "mvn clean compile"
			}
		}

		stage('Test') {
			steps{
				echo "Test"
				sh "mvn test"
			}
		}
		stage('Integration Test'){
			steps{
				echo "Integration Test"
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
	} 
	// post {
	// 	always {
	// 		echo "I'm awesome and i run always"
	// 		}
	// 	success {
	// 		echo "I run only when successful"
	// 		}
	// 	failure {
	// 		echo "I run only when fail"
	// 		}	
	// }
}
