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
            def dockerCmd = 'docker run  -p 3000:3000 -d ihnatsi/mbx:latest'
            sshagent(['ec2-frontend']) {
              sh "ssh -o StrictHostKeyChecking=no ec2-user@3.76.218.159 ${dockerCmd}"
            }
          } catch (err) {
            throw err
          }
        }
      }
    }
  }
}
