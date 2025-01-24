pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                checkout scm
            }
        }

        stage('Verify Directory') {
            steps {
                sh 'pwd'          // Print the current working directory
                sh 'ls -la'       // List all files in the current directory
                //sh 'ls -la deployment/' // List all files in the deployment directory
            }
        }

        stage('Verify Docker Installation') {
            steps {
                sh 'docker --version'         // Check Docker version
                sh 'docker-compose --version' // Check Docker Compose version
            }
        }

        stage('Build Docker Images') {
            steps {
              sh 'docker-compose -f /var/lib/jenkins/workspace/Mern/STAYFINDER-MERN_PROJECT/docker-compose.yml build'
              sh 'docker-compose -f /var/lib/jenkins/workspace/Mern/STAYFINDER-MERN_PROJECT/docker-compose.yml up -d'
            }
        }

        stage('Run Docker Containers') {
            steps {
                sh 'docker-compose -f /var/lib/jenkins/workspace/Mern/STAYFINDER-MERN_PROJECT/docker-compose.yml up -d'
            }
        }

        stage('Post-deployment Check') {
            steps {
                sh 'docker ps' // List running containers
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}
