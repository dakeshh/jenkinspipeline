pipeline{
    agent any
    stages{
        stage("Build") {
            steps {
                echo "Building...."
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
