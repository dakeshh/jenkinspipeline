pipeline{
    agent any
    environment {
        VERSION = "2.0.7-release"
        SERVER_CREDITIONAL = creditionals("dakeshh")
    }
    parameters {
        string(name: 'version1', defaultValue: '', description: "please provide input values ...")
        choice(name: 'version2', choices: ['1.0.1', '1.0.2', '1.0.3'], description: "please select version2")
        booleanParam(name: 'execteTest', defaultValue: true, description: "please select wanna execture test or not")
    }
    stages{
        stage("Build") {
            when {
                expression {
                    params.execteTest == true
                }
            }
            steps {
                echo "Building...."
                echo "Building version = ${VERSION}"
            }
        }
        stage("Test") {
            when {
                expression {
                    env.BRANCH_NAME == 'dev' || env.BRANCH_NAME == 'prod'
                }
            }
            steps {
                echo "Testing...."
            }
        }
        stage("Deploy") {
            steps {
                echo "Deploying...."
                echo "version1 =  ${version1}"
                echo "version2 = ${version2}"
            }
        }
    }
    post {
        always {
            echo "Always running ...."
            build 'test'
        }
        failure {
            echo "Running Failure jenkins job ...."
            build 'failure_test'
        }
        success {
            echo "Running success jenkins job ...."
            build 'success_test'
        }
    }
}
