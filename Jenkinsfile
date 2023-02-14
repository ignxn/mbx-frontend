node {
  try {
    stage('Build'){
     sh 'npm install'
    }
    stage('Deploy'){
      sh 'docker build -t react-app --no-cache .'
      sh 'docker tag react-app localhost:5000/react-app'
      sh 'docker push localhost:5000/react-app'
      sh 'docker rmi -f react-app localhost:5000/react-app'
    }
  }
  catch (err) {
    throw err
  }
}