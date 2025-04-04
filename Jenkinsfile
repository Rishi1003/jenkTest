pipeline {
    agent any

    environment {
        // Define environment variables based on your project needs
        PROJECT_NAME = 'your-project-name'
    }
    
    stages {
        stage('Test') {
            steps {
                echo 'Running tests...'
                }
            }
        }
        
        stage('Build') {
            steps {
                echo 'Building the application...'
        }
    }
    
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}