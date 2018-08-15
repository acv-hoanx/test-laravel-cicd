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
        sshagent(credentials: ['bae24a1e-e9f6-44c8-9d51-bdb42cf4bd60']) {
          sh 'ssh -o StrictHostKeyChecking=no -l root 192.168.2.5 uname -a -p 2122'
          sh 'ls -l'
        }
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