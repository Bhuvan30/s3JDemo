pipeline {
    agent any

    parameters {
        string(name: 'STACK_NAME', defaultValue: 'ec2-stack', description: 'CloudFormation Stack Name')
        string(name: 'TEMPLATE_FILE', defaultValue: '02_ec2cft.yml', description: 'CloudFormation Template File')
        string(name: 'INSTANCE_NAME', defaultValue: 'my-free-tier-ec2', description: 'EC2 Instance Name')
        choice(name: 'REGION', choices: ['eu-north-1'], description: 'AWS Region')
    }

    environment {
        AWS_DEFAULT_REGION = "${params.REGION}"
    }

    stages {
        stage('Checkout Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/riteshbehal/CloudFormation.git'
            }
        }

        stage('Deploy EC2 Stack') {
            steps {
                script {
                    echo "Deploying EC2 instance: ${params.INSTANCE_NAME} in region: ${params.REGION}"
                    sh """
                        aws cloudformation deploy \
                          --stack-name ${params.STACK_NAME} \
                          --template-file ${params.TEMPLATE_FILE} \
                          --region ${params.REGION} \
                          --capabilities CAPABILITY_NAMED_IAM \
                          --parameter-overrides InstanceName=${params.INSTANCE_NAME}
                    """
                }
            }
        }
    }
}
