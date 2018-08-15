pipeline {
  environment {
    DB_DATABASE = 'test-laravel-cicd'
    AA_SSH_KEY = credentials('e2068618-67f0-4edb-925e-a7aa7c7a4bad')
  }
  agent any
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