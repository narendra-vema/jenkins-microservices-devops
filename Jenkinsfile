pipeline {
    agent any
    // Define the pipeline stages
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
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
