pipeline {
    agent any
    tools { nodejs "14.16.0" }
    parameters {
        choice(name:'VERSION', choices:['1.0', '1.1', '1.2'], description:'Choose the version of the project')

        booleanParam(name :'executeTests', description:'Execute the tests', defaultValue:false)
    }

    stages {
        stage('Test') {
            steps {
                echo "Test"
            }
        }
    }
}
