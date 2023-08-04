pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                git credentialsId: 'Git', url: 'https://github.com/vamshikank9032/Jenkinscob.git'
            }
        }
        stage('sh') {
            steps {
               sh 'cd /home/ec2-user/git/Jenkinscob'
               sh './sample.sh'
            }
        }          
    }
}
