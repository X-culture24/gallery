pipeline {
    agent any

    environment {
        // MongoDB URI stored securely
        MONGO_URI = 'mongodb+srv://ARTHUR:Cristiano7!@cluster001.8kpqw.mongodb.net/?retryWrites=true&w=majority&appName=Cluster001'
        
        // Slack channel and webhook token for notifications
        SLACK_CHANNEL = '#lawrenceip1'
        SLACK_TOKEN = credentials('55dad864-fde5-4258-b45a-223bef1afbee') 
        
        // URL of the Render deployment
        RENDER_URL = 'https://gallery-d7kr.onrender.com'
    }

    triggers {
        // Automatically trigger the pipeline on a new commit to the repository
        githubPush() // Ensures Jenkins automatically triggers when a commit is pushed
    }

    stages {
        stage('Checkout Repository') {
            steps {
                script {
                    // Checkout the repository
                    checkout scm
                }
            }
        }

        

        stage('Install Dependencies') {
            steps {
                script {
                    // Install npm dependencies
                    sh 'npm install'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    // Run the tests with npm
                    sh 'npm test'
                }
            }
        }

        stage('Deploy to Render') {
            steps {
                script {
                    // Deploy the app to Render (assumes Render is set up for automatic deployment)
                    sh 'node server'
                }
            }
        }

        stage('Notify Slack') {
            steps {
                script {
                    // Notify Slack with the deployment success and details
                    slackSend (
                        channel: SLACK_CHANNEL,
                        color: 'good',
                        message: "Build Successful! Build ID: ${env.BUILD_ID}. Check the site here: ${RENDER_URL}"
                    )
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment to Render was successful.'
        }
        failure {
            echo 'Deployment failed. Please check the logs.'
        }
    }
}
