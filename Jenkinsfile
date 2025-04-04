pipeline {
    agent any

    environment {
        PROJECT_NAME = 'your-project-name' // Correct way to define variables
    }

    stages {
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }

        stage('Build') { // Moved inside stages block
            steps {
                echo 'Building the application...'
            }
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
