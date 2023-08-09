pipeline {
	//agent any
	agent {
		docker{
			image 'maven:latest'
		}
	}
	stages{
		stage('Build'){
			steps{
				sh 'mvn --version'
				echo "Build" 
			}
		}
		stage('Test'){
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
	post{
		always{
			echo "I am awesome"
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
