pipeline {
    agent any

    environment {
        DIRECTORY_PATH = '/var/lib/jenkins/workspace/Kaylin'
        TESTING_ENVIRONMENT = 'QA'
        PRODUCTION_ENVIRONMENT = 'Kaylin'
    }

    stages {
        stage('Build') {
            steps {
                echo "Fetch the source code from the directory path specified by the environment variable: ${env.DIRECTORY_PATH}"
                echo "Compile the code and generate any necessary artefacts"
            }
        }

        stage('Test') {
            steps {
                echo "Unit tests"
                echo "Integration tests"
            }
        }

        stage('Code Quality Check') {
            steps {
                echo "Check the quality of the code"
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploy the application to a testing environment specified by the environment variable: ${env.TESTING_ENVIRONMENT}"
            }
        }

        stage('Approval') {
            steps {
                echo "Waiting for manual approval..."
                sleep 10
                script {
                    input message: "Approve deployment to ${env.PRODUCTION_ENVIRONMENT} environment?", ok: "Deploy"
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "Deploying code to the production environment: ${env.PRODUCTION_ENVIRONMENT}"
            }
        }
        stage('Completed') {
            steps {
                echo "Completed..."
            }
        }
    }
}
