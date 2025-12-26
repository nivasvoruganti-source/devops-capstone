pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Images') {
            steps {
                sh 'docker compose -f docker-compose.yml build'

            }
        }

        stage('Run Containers') {
            steps {
                sh 'docker compose -f docker-compose.yml build'

            }
        }

        stage('Health Check') {
            steps {
                sh '''
                sleep 10
                curl http://localhost:5000/health
                '''
            }
        }
    }

    post {
        always {
            sh 'docker compose -f docker-compose.yml down'
        }
    }
}
