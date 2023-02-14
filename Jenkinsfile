pipeline {
    agent any
    tools {
        nodejs '14.16.0'
    }
    parameters {
        choice(name:'VERSION', choices:['1.0', '1.1', '1.2'], description:'Choose the version of the project')

        booleanParam(name :'executeTests', description:'Execute the tests', defaultValue:false)
    }

    stages {
        try {
            stage('Build') {
                steps {
                    sh 'npm install'
                }
            }
            stage('Test') {
                steps {
                    echo "Test"
                }
            }
            stage('Build Image') {
                steps {
                    withCredentials([usernamePassword(credentialsId: 'ihnatsi-docker-hub', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh 'docker build -t ihnatsi/mbx-frontend .'
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh 'docker push ihnatsi/mbx-frontend'
                    }
                }
            }
            stage ('Deploy') {
                steps {
                    script {
                        def dockerCmd = 'docker run  -p 3000:3000 -d ihnatsi/mbx-frontend:latest'
                        sshagent(['ec2-server-key']) {
                            sh "ssh -o StrictHostKeyChecking=no ec2-user@3.76.218.159 ${dockerCmd}"
                        }
                    }
                }
            }
        } catch(err) {
            throw err;
        }
    }
}
