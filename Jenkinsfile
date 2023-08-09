pipeline {
	agent any
	//agent { docker { image 'maven:3.6.3'}	}
	environment{
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages{
		stage('Checkout'){
			steps{
				sh 'mvn --version'
				sh 'docker --version'
				echo "Build" 
				echo "$PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "JOB_NAME - $env.JOB_NAME"
			}
		}
		stage('Compile'){
			steps{
				sh 'mvn clean compile'
			}
		}
		stage('Test'){
			steps{
				sh 'mvn failsafe:integration-test failsafe:verify'
			}
		}
		stage('Integration Test'){
			steps{
				echo "Integration Test"
			}
		}
		stage('Package'){
			steps{
				echo "mvn package -DskipTests"
			}
		}
		stage('Build Docker Image'){
			steps{
				//"docker build -t in28min/currency-exchange-devops:$env.BUILD_TAG"
				script{
					dockerImage = docker.build("nandanayak/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push Docker Image'){
			steps{
				script{
					docker.withRegistry('','dockerhub'){
						dockerImage.push()
						dockerImage.push('latest')
					}
				}
			}
		}
	} 
	post{
		always{
			echo "I am awesome always"
		}
		success{
			echo "I run when you are successful"
		}
		failure{
			echo "I run when you fail"
		}
		changed{
			echo "I changed"
		}
	}
	

}
