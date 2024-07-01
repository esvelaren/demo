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

        stage('Code Analyse: Lint') {
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
            when {
              branch "main"
            }
            steps {
                script {
                    echo 'Deploying application via ssh...'
                    // bat 'ssh user@server rm -rf /var/www/temp_deploy/dist/'
                    // bat 'ssh user@server mkdir -p /var/www/temp_deploy'
                    // bat 'scp -r dist user@server:/var/www/temp_deploy/dist/'
                    // bat 'ssh user@server "rm -rf /var/www/example.com/dist/ && mv /var/www/temp_deploy/dist/ /var/www/example.com/"'}
            }
        }
    }

    post {
        always {
            // Clean up workspace after build
            cleanWs()
            junit(allowEmptyResults: true, testResults: 'test-results/vitest-results.xml')
        }

        success {
            // Archive the 'dist' directory after a successful build
            archiveArtifacts artifacts: 'dist/**', fingerprint: true
            // Actions to take if the pipeline succeeds
            echo 'Build and deployment succeeded!'
        }

        failure {
            // Actions to take if the pipeline fails
            echo 'Build or deployment failed.'
        }
    }
}