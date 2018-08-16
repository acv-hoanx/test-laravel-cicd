pipeline {
  agent any
  environment {
    DB_DATABASE = 'test-laravel-cicd'
  }
  stages {
    stage('Build') {
      steps {
        echo 'BUILD STAGE'
        sh 'printenv'
      }
    }
    stage('Test') {
      steps {
        echo 'TEST STAGE'

        sshagent(['8faea60a-53f3-4e03-b9ee-90fb2e485c5b']) {
            sh 'ssh -p 2122 -o StrictHostKeyChecking=no root@192.168.2.5 uname -a'
            sh 'ssh -p 2122 -o StrictHostKeyChecking=no root@192.168.2.5 cd /var/www/html/proj_otocon; ls -l'
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