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
        stage('Develop') {
          when {
            branch 'develop'
          }
          steps {
            echo 'Deploy to tester'


          }
        }
        stage('Production') {
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