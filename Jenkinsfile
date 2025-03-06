pipeline {
   agent any
   stages{
    stage('CodeScan'){
        steps{
            sh 'trivy fs . -o result.html'
            sh 'cat result.html'
           
        }
    }
    stage('dockerLogin'){
        steps{
          sh 'aws ecr get-login-password --region us-east-1 | \
          docker login --username AWS \
          --password-stdin 381492114267.dkr.ecr.us-east-1.amazonaws.com'  
        }
    }
    stage('dockerImagesBuild'){
        steps{
            sh 'docker build -t jenkins-ci .'
            sh 'docker build -t imageversion'
        }
}
stage('dockerImageTag'){
    steps{
        sh 'docker tag jenkins-ci:latest \
        381492114267.dkr.ecr.us-east-1.amazonaws.com/jenkins-ci:latest'
        sh 'docker tag imageversion \
        381492114267.dkr.ecr.us-east-1.amazonaws.com/jenkins-ci:latest:v1.$BUILD_NUMBER'
    }
}
    stage('pushImage'){
        steps{
            sh 'docker push \
            381492114267.dkr.ecr.us-east-1.amazonaws.com/jenkins-ci:latest'
             sh 'docker push\
            381492114267.dkr.ecr.us-east-1.amazonaws.com/jenkins-ci:v1.$BUILD_NUMBER'

        }
    }
   } 

}