pipeline {
    agent any

    parameters {
        choice(
            name: 'DEPLOY_ENV',
            choices: ['development', 'testing', 'production'],
            description: 'Select the deployment environment'
        )
    }

    environment {
        APP_NAME = 'Jenkins-CICD-Lab'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    def buildScript = load 'scripts/buildInfo.groovy'
                    buildScript.displayBuildInfo()
                }

                bat 'java -version'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }

        stage('Use Credentials') {
            steps {
                withCredentials([
                    string(
                        credentialsId: 'demo-api-token',
                        variable: 'API_TOKEN'
                    )
                ]) {
                    echo 'API credential loaded successfully!'
                    bat 'if defined API_TOKEN (echo API token is available) else (echo API token is missing)'
                }
            }
        }

        stage('Deploy') {
            when {
                environment name: 'DEPLOY_ENV',
                          value: 'production'
            }
            steps {
                echo "Deploying ${APP_NAME} to ${params.DEPLOY_ENV}..."
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution finished.'
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}