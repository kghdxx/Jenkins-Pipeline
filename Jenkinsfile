// Jenkinsfile: theoretical-pipeline

pipeline {
    agent any

    environment {
        DIRECTORY_PATH = '/var/lib/jenkins/workspace/Kaylin'
        TESTING_ENVIRONMENT = 'QA'
        PRODUCTION_ENVIRONMENT = 'Kaylin'
        STAGING_SERVER = 'AWS EC2 Staging'
        PRODUCTION_SERVER = 'AWS EC2 Production'
        LOG_FILE = 'build-log.txt'
    }

    stages {
        stage('Build') {
            steps {
                sh """
                    echo "Stage 1: Build – Compile and package the code using Maven." | tee -a ${LOG_FILE}
                    echo "Simulating: mvn clean install" | tee -a ${LOG_FILE}
                """
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                sh """
                    echo "Stage 2: Unit and Integration Tests – Run tests using JUnit." | tee -a ${LOG_FILE}
                    echo "Simulating: Running JUnit tests" | tee -a ${LOG_FILE}
                """
            }
        }

        stage('Code Analysis') {
            steps {
                sh """
                    echo "Stage 3: Code Analysis – Analyse code using SonarQube." | tee -a ${LOG_FILE}
                    echo "Simulating: sonar-scanner" | tee -a ${LOG_FILE}
                """
            }
        }

        stage('Security Scan') {
            steps {
                sh """
                    echo "Stage 4: Security Scan – Scan for vulnerabilities using OWASP Dependency-Check." | tee -a ${LOG_FILE}
                    echo "Simulating: dependency-check --scan ." | tee -a ${LOG_FILE}
                """
            }
        }

        stage('Deploy to Staging') {
            steps {
                sh """
                    echo "Stage 5: Deploy to Staging – Deploy to test server (${env.STAGING_SERVER})." | tee -a ${LOG_FILE}
                    echo "Simulating: Deployment to ${env.STAGING_SERVER}" | tee -a ${LOG_FILE}
                """
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                sh """
                    echo "Stage 6: Integration Tests on Staging – Run Postman tests using Newman." | tee -a ${LOG_FILE}
                    echo "Simulating: newman run collection.json" | tee -a ${LOG_FILE}
                """
            }
        }

        stage('Approval') {
            steps {
                echo "Waiting for manual approval before production deployment..."
                sleep 10
                script {
                    input message: "Approve deployment to ${env.PRODUCTION_ENVIRONMENT} environment?", ok: "Deploy"
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                sh """
                    echo "Stage 7: Deploy to Production – Deploy to live server (${env.PRODUCTION_SERVER})." | tee -a ${LOG_FILE}
                    echo "Simulating: Deployment to ${env.PRODUCTION_SERVER}" | tee -a ${LOG_FILE}
                """
            }
        }

        stage('Completed') {
            steps {
                echo "Pipeline execution completed."
            }
        }
    }

    post {
        always {
            emailext(
                to: 'kaylin308@gmail.com',
                subject: "theoretical build - ${currentBuild.currentResult}: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "The pipeline executed and finished with status: ${currentBuild.currentResult}. See the attached log.",
                attachmentsPattern: "${env.LOG_FILE}"
            )
        }
    }
}
