pipeline {
  agent any
  environment {
    PATH_WEBROOT = '/var/www/html/proj_otocon'
  }
  stages {
    stage('Build') {
      steps {
        echo 'BUILD STAGE'
        sh 'printenv'
        sh 'php -v'
        sh 'php composer.phar --version'
        sh 'php composer.phar install'
      }
    }
    stage('Test') {
      steps {
        echo 'TEST STAGE'
        sh "./vendor/bin/phpunit"
        sshagent(['8faea60a-53f3-4e03-b9ee-90fb2e485c5b']) {
            sh 'ssh -p 2122 -o StrictHostKeyChecking=no root@192.168.2.5 cd $PATH_WEBROOT; ./scripts/deploy-develop.sh'
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