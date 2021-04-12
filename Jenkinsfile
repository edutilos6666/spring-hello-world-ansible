pipeline {
    agent any 
    parameters {
       choice(name: "selectedVersion", choices: ["1.0.0", "1.0.1", "1.1.0"], description: "User chooses the build version")
       booleanParam(name: "executeInit", defaultValue: true, description: "")
    }
    stages {
        stage("Dockerfile exists") {
            when {
                expression {
                    fileExists 'Dockerfile'
                }
                
            }
            
            steps {
             echo 'Dockerfile exists'   
            }
        }
        stage("send email") {
            steps {
                emailext body: '''<h1>Heading1</h1>
<h2>Heading2</h2>''', subject: 'test', to: 'edutilosaghayev@gmail.com'   
            }
            
            steps {
             mail bcc: '', body: '''hello world
<h1>Heading1</h1>
<h2>Heading2</h2>''', cc: '', from: '', replyTo: '', subject: 'test Mail', to: 'edutilosaghayev@gmail.com'   
            }
        }
        stage("build hello-world") {
            steps {
                build job: 'hello-world', parameters: [string(name: 'selectedVersion', value: '1.0.0'), booleanParam(name: 'executeInit', value: true)]   
            }
        }
        stage("init") {
            when {
                expression {
                    params.executeInit
                }
            }
            steps {
                withDockerContainer(image: 'maven',  toolName: 'Docker') {
                    // some block
                    sh 'mvn --version'
                }    
                echo "${env.BRANCH_NAME}"
                echo "${env.BUILD_NUMBER}"
                echo "selectedVersion = ${params.selectedVersion}"
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
