pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build stage'
      }
    }
    stage('Test') {
      steps {
        echo 'Test stage'
      }
    }
    stage('Deploy-Develop') {
      parallel {
        stage('Deploy-Develop') {
          when {
            branch 'develop'
          }
          steps {
            echo 'Deploy develop'
            sh 'composer -v'
          }
        }
        stage('Deploy-Production') {
          when {
            branch 'master'
          }
          steps {
            echo 'Deploy Production'
          }
        }
      }
    }
  }
}