pipeline {
    agent any

    environment {
        registry = "936445189194.dkr.ecr.eu-central-1.amazonaws.com/for-jenkins"
    }
   
    stages {
        
    
       
        stage("verity tooling") {
            steps{
                sh '''
                  docker version
                  docker info
                  docker compose version
                  curl --version
                  jq --version
                '''
            }
        }

          stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry
        }
      }
     }
      
        stage("start container") {
            steps {
                sh 'docker compose up -d --no-color --wait'
                sh 'docker compose ps'
            
            }
        }

          stage('Pushing to ECR') {
     steps{  
         script {
                sh 'aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin 936445189194.dkr.ecr.eu-central-1.amazonaws.com'
                sh 'docker push 936445189194.dkr.ecr.eu-central-1.amazonaws.com/for-jenkins:latest'
         }
        }
      }

        stage("run tests against container") {
            steps {
                sh 'curl http://localhost:8086/param?query=demo | jq'
            }
        }
    }
    
    
}

