pipeline {
    agent any 
    stages {
        stage("init") {
            steps {
                withDockerContainer(image: 'maven',  toolName: 'Docker') {
                    // some block
                    sh 'mvn --version'
                }    
            }
        }
        stage('Compile') {
            steps {
                echo 'Compiling the application!' 
            }
        }
        
        stage("Test"){
            steps {
                echo "Testing the application"
            }
        }
        
        stage("Build") {
            steps {
                echo "Building the application"
            }
        }
        
        stage("Docker Image Create") {
            steps {
               echo "Creating docker image"    
            }
        }
        
        stage("Docker Image Push") {
            steps {
                echo "Pushing docker image to the docker registry"    
            }
            
        }
    }
}
