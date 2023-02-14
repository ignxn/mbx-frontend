pipeline {
  agent any
  tools {
    nodejs '14.16.0'
  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }
    stage('Deploy') {
      steps {
        script {
          try {
            sh 'docker -v'
          } catch (err) {
            throw err
          }
        }
      }
    }
  }
}
