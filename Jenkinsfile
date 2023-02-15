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
    stage('Build Image') {
      steps {
        script {
          try {
            withCredentials([usernamePassword(credentialsId: 'docker-hub-ihnatsi', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
              sh 'docker build -t ihnatsi/mbx .'
              sh "echo $PASS | docker login -u $USER --password-stdin"
              sh 'docker push ihnatsi/mbx'
            }
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
            sh 'ls'
          } catch (err) {
            throw err
          }
        }
      }
    }
  }
}
