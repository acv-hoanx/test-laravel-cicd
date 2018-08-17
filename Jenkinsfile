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
        script {
          def comExists = fileExists 'composer.phar'
          if (!comExists) {
            sh 'php -r "copy(\'https://getcomposer.org/installer\', \'composer-setup.php\');"'
            sh 'php -r "if (hash_file(\'SHA384\', \'composer-setup.php\') === \'544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061\') { echo \'Installer verified\'; } else { echo \'Installer corrupt\'; unlink(\'composer-setup.php\'); } echo PHP_EOL;"'
            sh 'php composer-setup.php'
            sh 'php -r "unlink(\'composer-setup.php\');"'
          }
          sh 'php composer.phar --version'
          sh 'php composer.phar install'
          sh 'cp .env.example .env'
          sh 'php artisan key:generate'
        }
      }
    }
    stage('Test') {
      steps {
        echo 'TEST STAGE'
        script {
          if (comExists) {
            sh "./vendor/bin/phpunit"
          }
        }
        sshagent(['8faea60a-53f3-4e03-b9ee-90fb2e485c5b']) {
            sh 'ssh -p 2122 -o StrictHostKeyChecking=no root@192.168.2.5 bash $PATH_WEBROOT/scripts/deploy-develop.sh'
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