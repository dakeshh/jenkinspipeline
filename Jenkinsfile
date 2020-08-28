pipeline{
    agent any
    environment {
        VERSION = "2.0.7-release"
    }
    stages{
        stage("Build") {
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
