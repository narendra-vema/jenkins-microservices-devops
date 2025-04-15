pipeline {
    agent any
	// agent {
	// 	docker {
	// 		//image 'maven:3.6.3-jdk-8' // Use a Docker image with Maven and JDK 8
	// 		image 'node:14' // Use a Docker image with Node.js 14
	// 		// args '-v /var/run/docker.sock:/var/run/docker.sock' // Mount the Docker socket for Docker-in-Docker
	// 	}
	// }
	environment {
		// Define environment variables here
		dockerHome = tool "myDocker" // Use the Docker tool defined in Jenkins
		mavenHome = tool "myMaven" // Use the Maven tool defined in Jenkins
		PATH = "${dockerHome}/bin:${mavenHome}/bin:${env.PATH}" // Add Docker and Maven to the PATH
	}
    // Define the pipeline stages
    stages {
        stage('Checkout') {
            steps {
                //echo 'Building...'
				sh "mvn --version" // Print Maven version
				//sh "node --version" // Print Node.js version
				sh "docker --version" // Print Docker version
				echo 'Building...'
				echo '$PATH'
				echo 'BUILD_NUMBER is: ' + env.BUILD_NUMBER
				echo 'JOB_NAME is: ' + env.JOB_NAME
				echo 'WORKSPACE is: ' + env.WORKSPACE
				echo 'NODE_HOME is: ' + env.NODE_HOME
				echo 'PATH is: ' + env.PATH
				echo 'HOME is: ' + env.HOME
				echo 'PWD is: ' + env.PWD
				echo 'JENKINS_HOME is: ' + env.JENKINS_HOME
				echo 'JENKINS_URL is: ' + env.JENKINS_URL
				echo 'JENKINS_SERVER_COOKIE is: ' + env.JENKINS_SERVER_COOKIE
				echo '$env.BUILD_TAG is: ' + env.BUILD_TAG
				echo '$env.BUILD_URL is: ' + env.BUILD_URL
				echo '$env.JOB_URL is: ' + env.JOB_URL
            // Add your build steps here
            }
        }
		stage('Build') {
			steps {
                 sh "mvn clean compile" // Build the project using Maven
			// Add your build steps here
			}
		}

        stage('Test') {
            steps {
                echo 'mvn test...'
				sh "mvn test" // Run unit tests using Maven
            // Add your test steps here
            }
        }

        stage('integration Test') {
            steps {
                echo 'Integration Testing...'
            // Add your deployment steps here
            }
        }

		stage('create image') {
			steps {
			   // "docker build -t myapp:latest ." // Build a Docker image
               
			   script {
				// sh "mvn package -Dmaven.test.skip=true" // Package the application using Maven, skipping tests
 				  sh "mvn package -DskipTests" // Package the application using Maven, skipping tests
				   def image = docker.build("narendra230/currency-exchange-devops:${env.BUILD_ID}", "-f Dockerfile .") // Build a Docker image with a specific tag
				   echo "Docker image built: ${image}"
			   }							
			}
		}
		stage('Push image') {
			steps {
				echo 'Pushing Docker image...'
				docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') { // Authenticate with Docker Hub
					//sh "docker push narendra230/currency-exchange-devops:${env.BUILD_ID}" // Push the Docker image to Docker Hub
				    docker.image("narendra230/currency-exchange-devops:${env.BUILD_ID}").push() // Push the Docker image to Docker Hub
				}
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
