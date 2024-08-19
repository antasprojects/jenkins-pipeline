pipeline {
	agent any

	environment {
        dockerHome = tool "myDocker"
	  	mavenHome = tool "myMaven"
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
    }

	stages {
		stage('Build') {
			steps {
				sh "mvn --version"
				sh "docker --version"
				echo "Build"
				echo "Path: $PATH"
				echo "Build Number: $env.BUILD_NUMBER" 
				echo "Build ID: $env.BUILD_ID" 
				echo "Build Tag"
				echo "Build URL: $env.BUILD_URL" 
				echo "Job Name: $env.JOB_NAME" 
			}

			post {
				always {
					echo "Post Build"
				}
			}
		}
		stage("Compile") {
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test') {
			steps {
				sh "mvn test"
			}
		}
		stage('Integration Test') {
			steps {
				echo 'Integration Test'
			}
		}
		stage('Package') {
			steps {
				sh "mvn package -DskipTests"
			}
		}

		stage('Build Docker Image') {
			steps {
				// "docker build -t proasacio/currency-exchange:$env.BUILD_TAG"
				script {
					dockerImage = docker.build("proasacio/currency-exchange:${env.BUILD_TAG}")
				}
			}
		}

		stage('Push Docker Image') {
			steps {	
				script {
					docker.withRegistry("", 'docker-hub')
					dockerImage.push()
					dockerImage.push('latest')
				}
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