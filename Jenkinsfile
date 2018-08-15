pipeline {
  environment {
    DB_DATABASE = 'test-laravel-cicd'
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