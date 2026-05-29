pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = us-east-1
        S3_BUCKET = prajwal-static-website-2026
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/prajwal-rijo/my-static-site.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Static website build completed'
            }
        }

        stage('Deploy') {
            steps {
                withCredentials([
                    [
                        $class: 'AmazonWebServicesCredentialsBinding',
                        credentialsId: 'aws-creds'
                    ]
                ]) {

                    sh '''
                    aws s3 cp index.html s3://$S3_BUCKET/
                    '''
                }
            }
        }
    }
}
