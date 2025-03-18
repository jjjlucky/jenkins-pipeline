pipeline {
   agent any
   stages{
    stage('CodeScan'){
        steps{
            sh 'trivy fs . -o result.html'
            sh 'cat result.html'
        }
    }
    
    stage('dockerlogin'){
        steps{
            sh 'aws ecr get-login-password --region us-east-1 | \
            docker login --username AWS \
            --password-stdin 692859908343.dkr.ecr.us-east-1.amazonaws.com'
        }
    }
    stage('dockerImageBuild'){
        steps{
            sh 'docker build -t jenkins-ci .'
        }
}
stage('dockerImageTag'){
    steps{
        sh 'docker tag jenkins-ci:latest \
        692859908343.dkr.ecr.us-east-1.amazonaws.com/jenkins-ci:latest'
    }
}
    stage('pushImage'){
        steps{
            sh 'docker push \
            692859908343.dkr.ecr.us-east-1.amazonaws.com/jenkins-ci:latest'
        }
    }
   } 

}