pipeline {
    agent any

    environment {
        APP_ENV = 'staging'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                sh './build.sh'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh './run-tests.sh'
            }
        }

        stage('Deploy to Staging') {
            when {
                branch 'develop'
            }
            steps {
                echo "Deploying to staging environment"
                sh './deploy-staging.sh'
            }
        }

        stage('Deploy to Production') {
            when {
                branch 'main'
            }
            steps {
                input message: "Approve deployment to production?"
                echo "Deploying to production environment"
                sh './deploy-prod.sh'
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully.'
        }
        failure {
            echo 'Pipeline failed. Notifying team...'
            // Optional: send email/slack
        }
    }
}
