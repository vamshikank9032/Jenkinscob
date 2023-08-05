pipeline {
    agent any
    environment {
        AWS_REGION = 'us-east-2'
        STACK_NAME = 'sample-s3-CF'
        GIT_REPO_URL = 'https://github.com/vamshikank9032/Jenkinscob.git'
        GIT_BRANCH = 'Release'

    }
    stages {
        stage('Git Checkout') {
            steps {
              stash 'Source'
              git url: 'https://github.com/vamshikank9032/Jenkinscob.git'  
              sh "ls -lat"  
            //git branch: 'Release' credentialsId: 'Git', url: 'https://github.com/vamshikank9032/Jenkinscob.git'
            }
        }
        /*stage('sh') {
            steps {
               sh 'echo sh step executed'
               sh './sample.sh'
            }
        }*/
        stage('Deploy CF Template') {
           environment {
            AWS_ROLE_ARN = 'arn:aws:iam::737576955452:role/Role_For_Jenkins'
           } 

            steps {
                sh 'echo sh step executed'
                //sh 'echo "Validating template ${TEMPLATE_FILE}"'
                withAWS(role: "$arn:aws:iam::737576955452:role/Role_For_Jenkins") {
                    sh 'echo sh step executed'
                    sh 'echo sh step executed1'
                    sh 'echo sh step executed2'
                    sh 'cnvje=pwd'
                    sh 'echo $cnvje'
                    sh 'echo "Checking Name of stack ${STACK_NAME}"'
                    sh 'for file in `find .workspace/pipeline/cloudformation -name "*.yaml"`; do  echo "Validating template $file"; aws cloudformation validate-template --template-body "file://$file"; done'
                    //sh 'aws cloudformation validate-template --template-body file://${TEMPLATE_FILE}'
                //create stack
                sh """
                   sh 'echo sh step executed'
                   aws cloudformation deploy
                   --region ${AWS_REGION}
                   --stack-name ${STACK_NAME}
                   --template-file ${file}
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
