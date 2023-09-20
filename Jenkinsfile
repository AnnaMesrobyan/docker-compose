pipeline {
    agent any
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

       

        stage("start container") {
            steps {
                sh 'docker compose up -d --no-color --wait'
                sh 'docker compose ps'
            
            }
        }

        stage("run tests against container") {
            steps {
                sh 'curl http://localhost:3000/param?query=demo | jq'
            }
        }
    }
    
    
}

