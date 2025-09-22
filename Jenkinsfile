pipeline {
    agent any

    environment {
        NODE_VERSION = "18"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Kionbunny/ci-cd-react-project'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'No tests present. Skipping this stage.'
            }
        }

        stage('Build') {
            steps {
                bat 'npm run build'
            }
        }
        stage('Deploy to Vercel') {
            steps {
                // Use the stored Vercel token
                withCredentials([string(credentialsId: 'VERCEL_TOKEN', variable: 'VERCEL_TOKEN')]) {
                    bat 'npx vercel --prod --token %VERCEL_TOKEN%'
                }
            }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
