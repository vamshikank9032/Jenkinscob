pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'Git', url: 'https://github.com/vamshikank9032/Jenkinscob.git'
            }
        }
        stage('sh') {
            steps {
               sh 'ls'
               sh 'pwd'
               sh './sample.sh' 
            }
        }          
    }
}
