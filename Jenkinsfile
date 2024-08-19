pipeline {
	agent {
		docker {
			image 'node:21.7'
		}

	environment {
        DOCKER_HOST = 'tcp://localhost:2375'
        DOCKER_TLS_VERIFY = '0'
    }
	
	}
	stages {
		stage('Build') {
			steps {
				sh "node --version"
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