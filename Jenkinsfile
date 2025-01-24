pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                checkout scm
            }
        }

        stage('Verify Docker Compose Version') {
            steps {
                sh 'docker --version'
                sh 'docker-compose --version'
            }
        }

        stage('Build Docker Images') {
            steps {
                sh 'docker-compose -f /var/lib/jenkins/workspace/Mern/STAYFINDER-MERN_PROJECT/deployment/docker-compose.yml build'
            }
        }

        stage('Start Containers') {
            steps {
                sh 'docker-compose -f /var/lib/jenkins/workspace/Mern/STAYFINDER-MERN_PROJECT/deployment/docker-compose.yml up -d'
            }
        }

        stage('Post-deployment Check') {
            steps {
                sh 'docker ps'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}
