pipeline {
   agent any
   stages{
    stage('CodeScan'){
        steps{
            sh 'trivy fs . -o result.html'
           
        }
    }
    stage('dockerImagesBuild'){
        steps{
            sh 'docker -v'
        }
}
    stage('pushImage'){
        steps{
            sh 'docker ps'
        }
    }
   } 

}