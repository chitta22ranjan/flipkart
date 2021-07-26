pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "MAVEN 3.9.0"
    }
    environment {
	registry = "chitta22ranjan/chitta" 
        registryCredential = 'docker_key' 
        dockerImage = '' 
	}

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/chitta22ranjan/gamut.git'

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage('Building our image') { 
            steps { 
                script { 
                    dockerImage = docker.build registry  
                }

            } 
        }
        stage('upload our image') { 
            steps { 
                script { 
                    docker.withRegistry( '', registryCredential ) { 
                        dockerImage.push() 
                    }
                } 
            }

        }  
        
    }
}
