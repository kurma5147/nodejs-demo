pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('kurma5147')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/ravdy/nodejs-demo.git'
            }
        }
   
      stage('Docker build and push') {
      steps {
        sh '''
         whoami
	 echo $access_key
         aws configure set aws_access_key_id $access_key
         aws configure set aws_secret_access_key $secret_key
         aws configure set default.region us-east-1
         DOCKER_LOGIN_PASSWORD=$(aws ecr get-login-password  --region us-east-1)
         docker login -u AWS -p $DOCKER_LOGIN_PASSWORD https://381783421401.dkr.ecr.us-east-1.amazonaws.com
         docker build -t 381783421401.dkr.ecr.us-east-1.amazonaws.com/sample:SAMPLE-PROJECT-${BUILD_NUMBER} .
         docker push 381783421401.dkr.ecr.us-east-1.amazonaws.com/sample:SAMPLE-PROJECT-${BUILD_NUMBER}
          
        }   
    }
    
  }
 }
