pipeline {
    //agent any
	agent {
		label 'docker' // Use a specific agent with the label 'docker'
		docker {
			image 'maven:3.6.3-jdk-8' // Use a Docker image with Maven and JDK 8
			// args '-v /var/run/docker.sock:/var/run/docker.sock' // Mount the Docker socket for Docker-in-Docker
		}
	}
    // Define the pipeline stages
    stages {
        stage('Build') {
            steps {
                //echo 'Building...'
				sh "mvn --version" // Print Maven version
            // Add your build steps here
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
            // Add your test steps here
            }
        }

        stage('integration Test') {
            steps {
                echo 'Integration Testing...'
            // Add your deployment steps here
            }
        }
    } 
	
	post {
        always {
            echo 'This will always run after the stages.'
        }
        success {
            echo 'This will run only if the pipeline is successful.'
        }
        failure {
            echo 'This will run only if the pipeline fails.'
        }
        unstable {
            echo 'This will run if the pipeline is unstable.'
        }
		changed {
			echo 'This will run if the pipeline changes state.'
		}
    }
}
