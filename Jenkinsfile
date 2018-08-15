pipeline {
  environment {
    DB_DATABASE = 'test-laravel-cicd'
    DB_USERNAME = credentials('a5d8ff69-e76a-4ed3-ac6d-2bf3a94290c2')
  }
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'BUILD STAGE'
        sshagent(credentials: ['bae24a1e-e9f6-44c8-9d51-bdb42cf4bd60'], ignoreMissing: true) {
            // some block
            sh 'ls -l'
        }
      }
    }
    stage('Test') {
      steps {
        echo 'TEST STAGE'
        sh 'printenv'
      }
    }
    stage('Deploy') {
      parallel {
        stage('Deploy-Develop') {
          when {
            branch 'develop'
          }
          steps {
            echo 'Deploy to tester'


          }
        }
        stage('Deploy-Production') {
          when {
            branch 'master'
          }
          steps {
            echo 'DEPLOY PRODUCTION'
          }
        }
      }
    }
  }
}