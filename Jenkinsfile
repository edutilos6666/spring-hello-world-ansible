pipeline {
    agent any 
    environment {
         imageVersion = "${ENV.BUILD_ID}"
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
                    def springHelloWorldAnsible = docker.build("${env.imageName}:${env.imageVersion}")
                    docker.withRegistry("http://192.168.178.37:5000") {
                        springHelloWorldAnsible.push()
                    }
                }
            }
        }
        
        stage("Play ansible playbook in order to start docker container for this image") {
            steps {
                ansiblePlaybook credentialsId: 'elementary-os-vm-ssh-key', disableHostKeyChecking: true, installation: 'ansible', inventory: 'project.ini', playbook: 'deploy-docker.yml'
            }
        }
    }
}
