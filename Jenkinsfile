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
             def sshScript = '''
                echo "Transferring build folder"
                scp -i "${credentials(3.76.203.126)}" -r -P 22 ./build ec2-user@ec2-3-76-203-126.eu-central-1.compute.amazonaws.com:/var
            '''
            sh sshScript.trim()
          } catch (err) {
            throw err
          }
        }
      }
    }
  }
}
