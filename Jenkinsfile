pipeline {
    agent any
    
    stages {
        stage('clon repository') {
            steps {
                git credentialsId: 'GithubPAToken', url: 'https://github.com/MVLogix/Jenkins-DevOps.git', branch: 'ops1'
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

