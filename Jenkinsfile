pipeline {
    agent any
    triggers {
        pollSCM('H/5 * * * *') // Triggers every 5 minutes or on push
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/X-culture24/gallery.git', branch: 'main'
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    // Run npm install inside a Node.js Docker container
                    docker.image('node:16').inside {
                        sh 'npm install'
                    }
                }
            }
        }
        stage('Deploy to Render') {
            steps {
                script {
                    docker.image('node:16').inside {
                        sh 'node server.js'
                    }
                }
            }
        }
    }
}

