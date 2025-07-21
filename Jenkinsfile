//declarative

pipeline {

	agent any


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
				
				sh "mvn test"
			}
		}
		stage('Integration Test'){
			steps{
				
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}

		stage('package'){
			steps{
				
				sh "mvn package -DskipTests"
			}
		}

		stage('Build docker image'){
			steps{
				// "docker build -t yogi4rs/currency-exchange-devops:$env.BUILD_TAG"  this is directly writting the code
				// you can write using the inbuild script
				script{
					dockerImage = docker.build("yogi4rs/currency-exchange-devops:$env.BUILD_TAG")
				}
			}
		}
		stage('Push docker image'){
			steps{
				script{
					docker.withRegistry('', 'dockerhub'){
					dockerImage.push();
					dockerImage.push('latest');
					}
				}
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
