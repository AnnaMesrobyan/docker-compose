pipeline {
    agent any

    environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
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
        stage('Login') {
          steps {
        sh 'echo  dckr_pat_BCckauYYGBDayJJh5-0DIXCjQt | docker login -u annames1102 --password-stdin'
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

         

        stage("run tests against container") {
            steps {
                sh 'curl http://localhost:8086/param?query=demo | jq'
            }
        }
    }
    
    
}

