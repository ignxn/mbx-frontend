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
            sshagent(credentials: ['3.76.203.126']) {
             sh 'scp -r build ec2-user@ec2-3-76-203-126.eu-central-1.compute.amazonaws.com:/var'
            }
          } catch (err) {
            throw err
          }
        }
      }
    }
  }
}
