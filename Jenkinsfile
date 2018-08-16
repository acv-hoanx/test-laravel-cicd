pipeline {
  agent any
  environment {
    DB_DATABASE = 'test-laravel-cicd'
  }
  stages {
    stage('Build') {
      steps {
        echo 'BUILD STAGE'
        sh 'composer install'
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