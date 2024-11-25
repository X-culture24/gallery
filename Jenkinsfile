pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                script {
                    sh 'npm install'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    // Run tests using npm
                    sh 'npm test'
                }
            }
        }

        stage('Deploy to Render') {
            steps {
                script {
                    // Start the server with 'node server'
                    echo 'Deploying to Render...'
                    sh 'node server'
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment to Render and tests were successful!'
        }
        failure {
            echo 'Deployment or tests failed. Check the logs for details.'
            // Send an email or Slack notification if tests fail
        }
    }
}
