pipeline {
    agent any
    
    environment {
        // Environment variables
        NODE_ENV = 'production'
        NEXT_TELEMETRY_DISABLED = '1'
        // Use the Node.js installation in your Jenkins environment
        PATH = "${tool 'NodeJS'}/bin:${env.PATH}"
    }
    
    stages {
        stage('Prepare Environment') {
            steps {
                echo 'Checking Node and npm versions...'
                sh 'node --version'
                sh 'npm --version'
            }
        }
        
        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh 'npm ci'
            }
        }
        
        stage('Lint') {
            steps {
                echo 'Linting code...'
                sh 'npm run lint'
            }
        }
        
        stage('Tests') {
            steps {
                echo 'Running tests...'
                sh 'npm test'
            }
            post {
                always {
                    echo 'Tests completed'
                }
                success {
                    echo 'Tests passed!'
                }
                failure {
                    echo 'Tests failed!'
                }
            }
        }
        
        stage('Build') {
            steps {
                echo 'Building Next.js application...'
                sh 'npm run build'
            }
        }
        
        stage('Archive Artifacts') {
            steps {
                echo 'Archiving build artifacts...'
                archiveArtifacts artifacts: '.next/**/*', fingerprint: true
            }
        }
        
        stage('Deploy to Development') {
            when {
                branch 'develop'
            }
            steps {
                echo 'Deploying to development environment...'
                // Replace with your actual deployment command
                sh 'echo "Would deploy to development server here"'
            }
        }
        
        stage('Deploy to Production') {
            when {
                branch 'main'
            }
            steps {
                echo 'Deploying to production environment...'
                // Replace with your actual deployment command
                sh 'echo "Would deploy to production server here"'
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline execution completed'
        }
        success {
            echo 'Next.js build and deployment pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
            echo 'Consider sending a notification here'
        }
    }
}