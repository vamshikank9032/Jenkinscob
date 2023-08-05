pipeline {
    agent any
    environment {
        AWS_REGION = 'us-east-2'
        STACK_NAME = 'sample-s3-CF'
        TEMPLATE_FILE = './cloudformation'
        GIT_REPO_URL = 'https://github.com/vamshikank9032/Jenkinscob.git'
        GIT-BRANCH = 'Release'

    }
    stages {
        stage('Git Checkout') {
            steps {
              git url: 'https://github.com/vamshikank9032/Jenkinscob.git'  
            //git branch: 'Release' credentialsId: 'Git', url: 'https://github.com/vamshikank9032/Jenkinscob.git'
            }
        }
        stage('sh') {
            steps {
               sh 'cd /home/ec2-user/git/Jenkinscob'
               sh './sample.sh'
            }
        }
        stage('Deploy CF Template') {
           environment {
            AWS_ROLE_ARN = 'arn:aws:iam::737576955452:role/Role_For_Jenkins'
           } 

            steps {
                withAWS(role: "$arn:aws:iam::737576955452:role/Role_For_Jenkins") {
                    sh 'aws cloudformation validate-template --template-body file://${TEMPLATE_FILE}'
                //create stack
                sh """
                   aws cloudformation deploy
                   --region ${AWS_REGION}
                   --stack-name ${STACK_NAME}
                   --template-file ${TEMPLATE_FILE}
                   --capabilities CAPABILITY_IAM
                   --capabilities CAPABILITY_NAMED_IAM
                """
                }
            }
        }                   
    }
    post {
        success {
            echo "CloudFormation stack is deployed successfully"
        }
        failure {
            echo "CloudFormation stack failed"
        }
    }
}
