pipeline {
    agent any 
    environment {
         imageName = "spring-hello-world-ansible"
    }
    stages {
        stage("Checkout SCM") {
            steps {
                git 'https://github.com/edutilos6666/spring-hello-world-ansible.git'
            }
        }
        
        stage("Maven Compile & Test & Install")  {
            steps {
                sh "mvn install"
            }
        }
        
        stage("Build Docker image & push it to the registry") {
            steps  {
                 script {
                    def springHelloWorldAnsible = docker.build("${env.imageName}:${env.BUILD_ID}")
                    docker.withRegistry("http://192.168.178.37:5000") {
                        springHelloWorldAnsible.push()
                    }
                }
            }
        }
        
        stage("Play ansible playbook in order to start docker container for this image") {
            steps {
                ansiblePlaybook credentialsId: 'id_rsa_2', disableHostKeyChecking: true, installation: 'ansible', inventory: 'project.ini', playbook: 'deploy-docker.yml'
            }
        }
    }
}
