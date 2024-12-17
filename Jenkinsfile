pipeline {
    agent any

    environment {
        MONGO_URI = 'mongodb+srv://ARTHUR:Cristiano7!@cluster001.8kpqw.mongodb.net/?retryWrites=true&w=majority&appName=Cluster001'
        SLACK_CHANNEL = '#lawrenceip1'
        SLACK_TOKEN = credentials('55dad864-fde5-4258-b45a-223bef1afbee') 
        RENDER_URL = 'https://gallery-d7kr.onrender.com'
    }

    

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
                    
                    sh 'npm test'
                }
            }
        }

        stage('Deploy to Render') {
            steps {
                script {
                
                    sh 'node server'
                }
            }
        }

        stage('Notify Slack') {
            steps {
                script {
                    
                    slackSend (
                        channel: SLACK_CHANNEL,
                        color: 'good',
                        message: "Build Successful! Build ID: ${env.BUILD_ID}. Check the site here: ${https://gallery-d7kr.onrender.com}"
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
