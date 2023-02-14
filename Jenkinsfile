pipeline {
    agent any
    tools {
        nodejs 'nodejs'
    }
    parameters {
        choice(name:'VERSION', choices:['1.0', '1.1', '1.2'], description:'Choose the version of the project')
        booleanParam(name :'executeTests', description:'Execute the tests', defaultValue:false)
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                // sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                // sh 'npm run test'
                echo "Test"
            }
        }
        stage('Build Image') {
            steps {
                try {
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh 'docker build -t jennykibiri/sample-react-app .'
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh 'docker push jennykibiri/sample-react-app'
                    }
                } catch (err) {
                    // handle the error
                    echo "Error building and pushing Docker image: ${err.getMessage()}"
                    currentBuild.result = 'FAILURE'
                    error("Build failed: ${err.getMessage()}")
                }
            }
        }
        stage ('Deploy') {
            steps {
                try {
                    script {
                        def dockerCmd = 'docker run  -p 3000:3000 -d jennykibiri/sample-react-app:latest'
                        sshagent(['ec2-server-key']) {
                            sh "ssh -o StrictHostKeyChecking=no ec2-user@3.92.144.96 ${dockerCmd}"
                        }
                    }
                } catch (err) {
                    // handle the error
                    echo "Error deploying Docker image: ${err.getMessage()}"
                    currentBuild.result = 'FAILURE'
                    error("Deployment failed: ${err.getMessage()}")
                }
            }
        }
    }
}
