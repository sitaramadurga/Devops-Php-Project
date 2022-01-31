pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
               git branch: 'main', url: 'https://github.com/sitaramadurga/Devops-Php-Project.git'
            }
        }
        stage('Docker Build'){
            steps{
                sh "docker build . -t sitaa8h/my-php-website"
            }
        }
        stage('DockerHub Push'){
            steps{
                
                withCredentials([string(credentialsId: 'docker-hub', variable: 'dockerPwd')]) {
                      sh "docker login -u sitaa8h -p ${dockerPwd}"
                }
                
                sh "docker push sitaa8h/my-php-website "
            }
        }
        stage('Install Python 3') {
            steps {
               ansiblePlaybook credentialsId: 'test-server', installation: 'ansible', inventory: 'servers.inv', playbook: 'python3-playbook.yml'
            }
        }
         stage('Install docker and its dependencies and run contianer') {
            steps {
               ansiblePlaybook credentialsId: 'test-server', installation: 'ansible', inventory: 'servers.inv', playbook: 'deployment-playbook.yml'
            }
        }
    }
}

