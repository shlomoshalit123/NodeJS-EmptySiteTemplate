pipeline {
  agent any
  stages {
    stage('chekout code') {
      parallel {
        stage('chekout code') {
          steps {
            git(url: 'git@github.com:lidorg-dev/NodeJS-EmptySiteTemplate.git', branch: 'master', credentialsId: 'github')
          }
        }

        stage('say hello to me ') {
          steps {
            sh 'echo "Hello"'
          }
        }

      }
    }

    stage('Build') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test App') {
      parallel {
        stage('Run the App') {
          steps {
            sh 'node server.js'
          }
        }

        stage('check if app is running') {
          steps {
            sh '''sleep 5
curl localhost:8081 
if [[ $(echo $?) -eq 0 ]]; 
then
  echo "success" 
  ps -ef | grep node | awk \'{print $2}\' | xargs kill
  exit 0
else 
  echo "failure"
  exit 1
fi  '''
          }
        }

      }
    }

  }
}