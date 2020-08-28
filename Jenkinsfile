pipeline{
    agent any
    stages{
        stage("Build"){
            steps{
                echo "Building...."
            }
        }
        stage("Test"){
            steps{
                echo "Testing...."
            }
        }
        stage("Deploy"){
            steps{
                echo "Deploying...."
                build 'test'
            }
        }
    }
    post {
        failure {
            steps {
                echo "Running Failure jenkins job ...."
                build 'failure_test'
            }
        }
        success {
            steps {
                echo "Running success jenkins job ...."
                build 'success_test'
            }
        }
    }
}
