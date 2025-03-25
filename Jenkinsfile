pipeline {
    agent any
    
    stages {
        stage('clon repository') {
            steps {
                git credentialsId: 'GithubPAToken', url: '', branch: 'ops1'
            }
        }
        
        stage('install dependencies') {
            steps {
                script {
                    sh 'npm install'
                }
            }
        }
        
        stage('build react app') {
            steps {
                script {
                    sh 'npm run build'
                }
            }
        }

	stage('deploy to s3') {
            steps {
                withAWS(region: 'ap-south-1', credentials: 'aws_access_key_token') {
                    sh 'aws s3 cp ./dist s3://apach2-srv-data-btk/ --recursive'
                }
            }
        }
        
        stage('Invalidate CloudFront Cache') {
            steps {
                withAWS(region: 'ap-south-1', credentials: 'aws_access_key_token') {
                    sh 'aws cloudfront create-invalidation --distribution-id E1EN3557XUAINU --paths "/*"'
                }
            }
        }
        
    }
    
    post {
        success {
            echo "Deployment Successful!"
        }

        failure {
            echo "Deployment Failed!"
        }
    }
}

