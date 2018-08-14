pipeline {
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