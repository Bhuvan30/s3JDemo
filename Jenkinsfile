pipeline {
    agent any

    environment {
        STACK_NAME = "S3BucketStack"
        TEMPLATE_FILE = "s3-bucket-param.yaml"
        REGION = "us-east-1"
        BUCKET_NAME = "my-jenkins-bucket-${BUILD_NUMBER}"
    }

    stages {
        stage('Deploy CloudFormation') {
            steps {
                script {
                    sh """
                    aws cloudformation deploy \
                      --template-file ${TEMPLATE_FILE} \
                      --stack-name ${STACK_NAME} \
                      --region ${REGION} \
                      --capabilities CAPABILITY_NAMED_IAM \
                      --parameter-overrides S3BucketName=${BUCKET_NAME}
                    """
                }
            }
        }
    }
}
