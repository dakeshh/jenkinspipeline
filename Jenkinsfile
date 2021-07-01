// Define a groovy local variable, myVar.
// A global variable without the def, like myVar = 'initial_value',
// was required for me in older versions of jenkins. Your mileage
// may vary. Defining the variable here maybe adds a bit of clarity,
// showing that it is intended to be used across multiple stages.
def myVar = 'initial_value'

pipeline{
    agent any
    environment {
        VERSION = "2.0.7-release"
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
        stage('Build_Main') {
            steps {
                sh 'make' 
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true 
            }
        }
        stage('Four') {
            parallel { 
                   stage('Unit Test') {
                       steps {
                            echo "Running the unit test..."
                       }
                   }
                   stage('Integration test') {
                      agent {
                            docker {
                                    reuseNode true
                                    image 'ubuntu'
                                   }
                            }
                      steps {
                        echo "Running the integration test..."
                      }
                   }
              }
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
