pipeline{
  agent any
  stages{
    stage('Checkout Out'){
      steps{
        git branch: 'main', url: 'https://github.com/Emmy-S-300/test-django'
      }
    }
    stage('Login to ECR'){
      steps{
        withAWS(region: 'us-east-1', credentials: "aws-creds"){
          sh '''
          aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 745490702538.dkr.ecr.us-east-1.amazonaws.com
          '''
        }
      }
    }
    stage('Build docker image'){
      steps{
        sh '''
        docker build -t test:django .
        docker tag test:django 745490702538.dkr.ecr.us-east-1.amazonaws.com/test:django
        '''
      }
    }
    stage('Pushing image to ECR'){
      steps{
        sh '''
        docker push 745490702538.dkr.ecr.us-east-1.amazonaws.com/test:django
        '''
      }
    }
  }
}
