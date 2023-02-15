pipeline {
  agent any
  tools {
    nodejs '14.16.0'
  }
  stages {
    stage('Build') {
      steps {
        script {
          try {
            sh 'npm install'
          } catch(err) {
            throw err;
          }
        }
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
