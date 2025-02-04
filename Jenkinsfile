pipeline {
    agent any

    environment {
        CI = 'true'
    }

    tools {
        nodejs '22.3.0'
    }

    stages {
        stage('Install Dependencies') {
            steps {
                script {
                    // Use Node.js environment
                    bat 'node --version'
                    bat 'npm --version'
                    bat 'npm cache clean --force'
                    bat 'npm install --verbose'
                }
            }
        }

        stage('Lint') {
            steps {
                script {
                    // Run linting, assuming a script named "lint" is defined in package.json
                    bat 'npm run lint'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Run tests, assuming a script named "test" is defined in package.json
                    bat 'npm run test'
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Build the project, assuming a script named "build" is defined in package.json
                    bat 'npm run build'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Add deployment script here
                    // This is a placeholder for deployment commands
                    // For example, to deploy using SSH or to a cloud provider
                    echo 'Deploying application...'
                    // sh 'deploy-command-here'
                }
            }
        }
    }

    post {
        always {
            // Clean up workspace after build
            cleanWs()
        }

        success {
            // Actions to take if the pipeline succeeds
            echo 'Build and deployment succeeded!'
        }

        failure {
            // Actions to take if the pipeline fails
            echo 'Build or deployment failed.'
        }
    }
}