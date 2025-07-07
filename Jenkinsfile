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
          $loginCommand = aws ecr get-login --no-include-email --region us-east-1
          Invoke-Expression $loginCommand
          '''
        }
      }
    }
    stage('Build docker image'){
      steps{
        sh '''
        docker build - t test:django
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
