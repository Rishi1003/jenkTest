pipeline {
    agent any

    environment {
        NODE_ENV = 'production'
        AWS_ACCESS_KEY_ID = "test"
        AWS_SECRET_ACCESS_KEY = "test"
        DB_URL = 'your-db-url-here'
    }

    triggers {
        scm('H/5 * * * *')  // Poll SCM every 5 mins
        cron('H 2 * * *')   // Daily build at 2 AM
    }

    options {
        timestamps()
        skipDefaultCheckout()
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    echo 'Cloning repository...'
                }
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    echo 'Installing dependencies...'
                    sh 'npm ci'
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    echo 'Building Next.js app...'
                    sh 'npm run build'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo 'Setting up test database...'
                    // Simulate DB setup
                    echo "Connected to DB: ${env.DB_URL}"

                    echo 'Running test scripts (placeholder)...'
                    // sh 'npm run test'  // Uncomment if test scripts exist
                }
            }
        }

        stage('Deploy to AWS') {
            steps {
                script {
                    echo 'Deploying to AWS (mock steps)...'
                    // Example: Upload build to S3 or trigger deploy with CLI
                    // sh 'aws s3 sync .next/ s3://your-bucket-name'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check logs.'
        }
        always {
            echo 'Cleaning up...'
            cleanWs()
        }
    }
}
