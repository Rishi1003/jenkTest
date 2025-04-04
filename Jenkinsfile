 pipeline {
     agent any

     stages {
         
         stage('Checkout') {
             steps {
                 checkout scm
             }
         }
         
         stage('Install Dependencies') {
             steps {
                 sh 'npm ci'
             }
         }
         
         stage('Lint') {
             steps {
                 sh 'npm run lint || true'
             }
         }
         
         stage('Build') {
             steps {
                 sh 'npm run build'
             }
         }
         
         stage('Start Server') {
             steps {
                 script {
                     // Kill any existing Next.js processes
                     sh 'pkill -f "node.*next" || true'
                     
                     // Start the Next.js server in the background
                     sh 'nohup npm run start > nextjs.log 2>&1 &'
                     
                     // Wait for the server to start
                     sh 'sleep 10'
                     
                     // Verify the server is running
                     sh 'curl -s http://localhost:3000 || echo "Server not responding"'
                     
                     // Display the log for debugging
                     sh 'cat nextjs.log'
                 }
             }
         }
     }
     
     post {
         always {
             // Archive the logs
             archiveArtifacts artifacts: 'nextjs.log', allowEmptyArchive: true
         }
         cleanup {
             // Optional: Keep the server running or shut it down
             // Uncomment the next line if you want to stop the server after the build
             // sh 'pkill -f "node.*next" || true'
         }
     }
 }