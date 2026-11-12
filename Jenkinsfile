
pipeline {
    agent any

    environment {
        DEPLOY_ENV = 'production'
        APP_NAME = 'Jenkins-CICD-Lab'
    }

    stages {
        stage('Build') {
            steps {
                echo "Building ${APP_NAME}..."
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }

        stage('Deploy') {
            when {
                environment name: 'DEPLOY_ENV',
                          value: 'production'
            }
            steps {
                echo "Deploying ${APP_NAME} to ${DEPLOY_ENV}..."
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
