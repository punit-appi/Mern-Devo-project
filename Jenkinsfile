pipeline {
    agent any
    environment {
        NODE_ENV = 'production'
    }
    tools {
        nodejs 'nodejs' // Make sure 'nodejs' is the name of your Node.js installation in Jenkins
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/punit-appi/Mern-Devo-project.git'
            }
        }
        stage('Install Backend Dependencies') {
            steps {
                dir('backend') {
                    sh 'npm install'
                    sh script: 'pm2 reload ecosystem.config.js || pm2 start ecosystem.config.js', cwd: pwd()
                }
            }
        }
        stage('Install Frontend Dependencies') {
            steps {
                dir('frontend') {
                    sh 'npm install'
                }
            }
        }
        stage('Build Frontend') {
            steps {
                dir('frontend') {
                    sh 'npm run build'
                }
            }
        }
        stage('Run Backend Tests') { // Uncomment if you have backend tests
            steps {
                dir('backend') {
                    sh 'npm test'
                }
            }
        }
        stage('Run Frontend Tests') { // Uncomment if you have frontend tests
            steps {
                dir('frontend') {
                    sh 'npm test'
                }
            }
        }
        stage('Deploy Application') {
            steps {
                script {
                    // Deploy backend
                    dir('backend') {
                        sh 'pm2 stop all || true' // Stop any existing PM2 processes
                        sh script: 'pm2 start ecosystem.config.js', cwd: pwd()
                    }
                    // Deploy frontend
                    dir('frontend') {
                        sh "cp -r build/* /var/www/html" // ***REPLACE THIS WITH YOUR ACTUAL DEPLOYMENT PATH***
                    }
                }
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the logs for details.'
        }
    }
}
