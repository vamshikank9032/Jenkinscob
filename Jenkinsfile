pipeline {
    agent any
    environment {
        AWS_DEFAULT_REGION = 'us-east-2'
        STACK_NAME = 'sample-s3-CF1'
        GIT_REPO_URL = 'https://github.com/vamshikank9032/Jenkinscob.git'
        GIT_BRANCH = 'Release'
        IAM_ROLE_ARN = 'arn:aws:iam::737576955452:role/Role_For_Jenkins'
        TEMPLATE_FILE = 's3.yaml'
    }
    stages {
        stage('Git Checkout') {
            steps {
              //stash 'Source'
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
                steps {
                //sh 'echo sh step executed'
                //sh 'echo "Validating template ${TEMPLATE_FILE}"'
                //withCredentials([[$class:'AmazonWebServicesCredentialsBinding',credentialsId: "IAM_USER", accessKeyVariable: 'AWS_ACCESS_KEY_ID', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']])
                 //withAWS(region: "${AWS_REGION}", credentials: "${IAM_ROLE}"){
                 //withAWS(role: "${IAM_ROLE_ARN}") {
                    sh 'echo "Running cfn template Validation"'
                    //sh pwd
                    //sh 'for file in `find ./workspace/pipe/cloudformation/ -name "*.yaml"`; do  echo "Validating template $file"; aws cloudformation validate-template --template-body "file://$file"; done'
                    //sh 'aws cloudformation validate-template --template-body file://${TEMPLATE_FILE}'
                //create stack
                sh """
                   ls
                   pwd
                   aws cloudformation deploy --region ${AWS_DEFAULT_REGION} --template-file sb3.yaml --stack-name sample-s3-CF1             
                   --capabilities CAPABILITY_IAM --capabilities CAPABILITY_NAMED_IAM ----parameter-overrides PREPROD
                """
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
