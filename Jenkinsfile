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
            sh 'rm -rf node_modules'
            sh 'ls -a'
            sh 'npm install'
            sh 'ls -a'
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
            sh 'ls -a'
          } catch (err) {
            throw err
          }
        }
      }
    }
  }
}
