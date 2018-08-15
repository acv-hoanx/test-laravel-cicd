pipeline {
  environment {
    DB_DATABASE = 'test-laravel-cicd'
    AA_SSH_KEY = credentials('bae24a1e-e9f6-44c8-9d51-bdb42cf4bd60')
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
      node {
        def remote = [:]
        remote.name = 'test'
        remote.allowAnyHosts = true
        remote.host = '192.168.2.5'
        remote.user = 'root'
        remote.port = 2122
        remote.identity = credentials('bae24a1e-e9f6-44c8-9d51-bdb42cf4bd60')
        stage('Remote SSH') {
            sshCommand remote: remote, command: "ls -lrt"
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