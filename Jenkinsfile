pipeline {
    agent any

    environment {
        registry = "936445189194.dkr.ecr.eu-central-1.amazonaws.com/for-jenkins"
    }
   
    stages {
        stage('Cloning Git') {
            steps {
                checkout scmGit(branches: [[name: '*/AnnaMesrobyan-main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/AnnaMesrobyan/docker-compose.git']])    
            }
        }
    
       
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

        stage("prune docker data") {
            steps {
                sh 'docker system prune -a --volume -f'

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

