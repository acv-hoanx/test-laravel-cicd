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
        sh 'composer install'
        sh 'php artisan vendor:publish --all'
      }
    }
    stage('Test') {
      steps {
        echo 'TEST STAGE'
        sh 'printenv'
      }
    }
    stage('Deploy-Develop') {
      parallel {
        stage('Deploy-Develop') {
          when {
            branch 'develop'
          }
          steps {
            echo 'DEPLOY DEVELOP'

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