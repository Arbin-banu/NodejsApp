pipeline {
    agent any

    stages {
         stage('build') {
            steps {
                sh 'docker build -t arbinecr .'
            }
        }
        stage('push') {
            steps {
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 327762787891.dkr.ecr.us-east-1.amazonaws.com'
                sh 'docker tag arbinecr:latest 327762787891.dkr.ecr.us-east-1.amazonaws.com/ecr-nodejs:latest'
                sh 'docker push 327762787891.dkr.ecr.us-east-1.amazonaws.com/ecr-nodejs:latest' 
            }
        }
        stage('deploy'){
            steps{
                sh 'docker run -d --name nodejs-app -p 8080:8081 327762787891.dkr.ecr.us-east-1.amazonaws.com/ecr-nodejs:latest'
            }
        }

    }
}
