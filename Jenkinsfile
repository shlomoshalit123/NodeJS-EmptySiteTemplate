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
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
              sh 'node server.js'
            }

          }
        }

        stage('check if app is running') {
          steps {
            sh '''sleep 5
curl localhost:8081 
if [ $(echo $?) -eq 0 ]; 
then
  echo "success" 
  ps -ef | grep node | awk \'{print $2}\' | head -n 1 | xargs kill
  exit 0
else 
  echo "failure"
  exit 1
fi  '''
          }
        }

      }
    }

    stage('Package') {
      steps {
        sh '''mkdir bin && mv * bin/
tar -czvf package-$BUILD_ID.tar.gz bin/
'''
      }
    }

    stage('Archive Artifact') {
      steps {
        archiveArtifacts '*.tar.gz'
        sh 'rm -rf *'
      }
    }

  }
}