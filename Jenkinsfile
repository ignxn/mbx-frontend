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
             def sshKey = credentials('3.76.203.126') // replace with the ID of your SSH credential
             def sshHost = '3.76.203.126' // replace with your SSH server hostname or IP address
             def sshUser = 'ec2-user' // replace with your SSH username
             def sshPort = 22 // replace with your SSH server port number
             def remoteDir = '/' // replace with the remote directory path where you want to transfer the build folder

             def scpCmd = "scp -i ${sshKey} -r -P ${sshPort} ./build ${sshUser}@${sshHost}:${remoteDir}"

             sh """
                 echo \"Transferring build folder\"
                 ${scpCmd}
             """
          } catch (err) {
            throw err
          }
        }
      }
    }
  }
}
