pipeline {
	agent {
		docker {
			image 'maven:3.9.6'
		}
	}
	stages {
		stage('Build') {
			steps {
				sh "mvn --version"
				echo "Build"
			}

			post {
				always {
					echo "Post Build"
				}
			}
		}
		stage('Test') {
			steps {
				echo "Test"
			}
		}
		stage('Integration Test') {
			steps {
				echo 'Integration Test'
			}
		}
	}
	post {
		always {
			echo 'I always run'
		}
		success {
			echo "I run when successful"
		}
		failure {
			echo "I run when failed"
		}
	}
}