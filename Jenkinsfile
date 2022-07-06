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
      steps {
        sh 'node server.js'
      }
    }

  }
}