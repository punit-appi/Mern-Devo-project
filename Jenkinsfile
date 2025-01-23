pipeline {
    agent any
    environment {
        NODE_ENV = 'production'
    }
    tools {
        nodejs 'nodejs' // Specify the Node.js version configured in Jenkins
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
                    sh 'pm2 start ecosystem.config.js'
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
        // Uncomment to run backend tests
        // stage('Run Backend Tests') {
        //     steps {
        //         dir('backend') {
        //             sh 'npm test'
        //         }
        //     }
        // }
        // Uncomment to run frontend tests
        // stage('Run Frontend Tests') {
        //     steps {
        //         dir('frontend') {
        //             sh 'npm test'
        //         }
        //     }
        // }
        stage('Deploy Application') {
            steps {
                script {
                    // Deploy backend
                    dir('backend') {
                        sh 'pm2 stop all || true'
                        sh 'pm2 start npm -- start --name "mern-backend"'
                    }
                    // Deploy frontend
                    dir('frontend') {
                        sh 'cp -r build/* /path/to/frontend/deployment/directory'
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
