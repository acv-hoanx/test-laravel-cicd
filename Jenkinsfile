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
          steps {
            echo 'Deploy develop'
            sh 'composer -v'
          }
        }
        stage('Deploy-Production') {
          steps {
            echo 'Deploy Production'
          }
        }
      }
    }
  }
}