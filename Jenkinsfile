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
                
                withCredentials([string(credentialsId: 'dockerPwd', variable: 'dockerPwd')]) {
                      sh "docker login -u sitaa8h -p ${dockerPwd}"
                }
                
                sh "docker push sitaa8h/my-php-website"
            }
        }

         stage('Install docker and its dependencies and run contianer') {
            steps {
                sh "ansible-playbook playbook.yml -i servers.inv"
            }
        }
    }
}

